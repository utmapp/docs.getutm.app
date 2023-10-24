---
layout: default
title: Troubleshooting a VM
parent: Advanced
---
## What is a Debug Log?

When you encounter an error message in UTM, it is often helpful to enable and export a so-called Debug Log for the VM. This is a text file that contains information about how you configured the VM and which warnings and errors occurred in the backend while it was running.

**This Debug Log is required when submitting a new Issue relating to a VM problem. If you don't yet have the Debug Log, please get it before creating the issue. It is very easy to do and will help you and others understand and fix the problem.**

**Note:** This does not apply to Apple Silicon VMs (running either macOS or Linux using Apple's Virtualization). There is no debug log option for these VMs.

## When do I not need to get a Debug Log?

You do not need to get a Debug Log for your issue in the following cases:

- problem exists before VM is started (before you click Play)
- User Interface issue that happens with every VM
- UTM crash while a VM is not running (must provide crash log - copy from the macOS popup)

## How to get Debug Log?

1. open UTM
2. select the VM that has the problem
3. click the top right (edit) button to open the VM Configuration window
4. select the QEMU tab
5. enable Debug Logging
6. click Save
7. click Play to start the VM
8. wait for the VM to show the problem
9. close the VM window
10. open Configuration again
11. select QEMU tab again
12. click Export Debug Log…
13. save file to your Desktop

## How to read Debug Log

### VM Configuration and QEMU Arguments

The first line in the log (starts with `Running:`) contains the QEMU arguments that UTM has created based on your UTM VM Configuration. QEMU is part of the backend for UTM. Example:

```log
Running:  -L /Applications/UTM.app/Contents/Resources/qemu -S -qmp tcp:127.0.0.1:4000,server,nowait -nodefaults -vga none -spice "unix=on,addr=/Users/chris/Library/Group Containers/WDNLXAD4W8.com.utmapp.UTM/E582C6D5-8ABB-4C23-8F5E-075C842F14B0.spice,disable-ticketing=on,image-compression=off,playback-compression=off,streaming-video=off,gl=on" -device virtio-ramfb -cpu host -smp cpus=1,sockets=1,cores=1,threads=1 -machine virt-6.1,highmem=off -accel hvf -accel tcg,tb-size=1024 -bios /Applications/UTM.app/Contents/Resources/qemu/edk2-aarch64-code.fd -boot menu=on -m 4096 -device ich9-intel-hda -device hda-duplex -name "Ubuntu ARM 2.2.0" -device qemu-xhci,id=usb-bus -device usb-tablet,bus=usb-bus.0 -device usb-mouse,bus=usb-bus.0 -device usb-kbd,bus=usb-bus.0 -device qemu-xhci,id=usb-controller-0 -chardev spicevmc,name=usbredir,id=usbredirchardev0 -device usb-redir,chardev=usbredirchardev0,id=usbredirdev0,bus=usb-controller-0.0 -device usb-storage,drive=drive0,removable=true,bootindex=0 -drive if=none,media=cdrom,id=drive0 -device virtio-blk-pci,drive=drive1,bootindex=1 -drive "if=none,media=disk,id=drive1,file=/Users/chris/Library/Containers/com.utmapp.UTM/Data/Documents/Ubuntu ARM 2.2.0.utm/Images/disk-0.qcow2,cache=writethrough" -device virtio-net-pci,mac=9E:FF:F7:C9:01:AF,netdev=net0 -netdev vmnet-macos,mode=bridged,id=net0 -device virtio-serial -device virtserialport,chardev=vdagent,name=com.redhat.spice.0 -chardev spicevmc,id=vdagent,debug=0,name=vdagent -uuid E582C6D5-8ABB-4C23-8F5E-075C842F14B0 -rtc base=localtime
```

This line is very important for figuring out if your problem is caused by an incompatible configuration.

For example, let's say we are trying to run Windows XP. You can't run Windows XP while using the EFI boot option, and in the example above the `-bios /Applications/UTM.app/Contents/Resources/qemu/edk2-aarch64-code.fd` part shows that the EFI boot option is selected.

### Information Messages and Warnings

Any number of lines may appear in the Debug Log, and it does not necessarily indicate a problem.

For example, the line `qemu-aarch64-softmmu: -netdev vmnet-macos,mode=bridged,id=net0: info: Started vmnet interface with configuration:` means you selected the Shared or Bridged Mode in the Network tab. This is normal and not an error (as indicated by the "info:" part).

### Errors

If you get an error popup in UTM, the error and more information will be in the last lines of the Debug Log. For example, an error occurred and this is from the end of the log file:

```log
vrend_compile_shader: context error reported 2 "Xorg" Illegal shader 0
shader failed to compile
ERROR: 0:11: 'fsout_c0' : must explicitly specify all locations when using multiple fragment outputs
ERROR: 0:13: 'fsout_c1' : must explicitly specify all locations when using multiple fragment outputs

fs: 47 GLSL:
   1: #version 300 es
…
```

This error alone is not sufficient to pinpoint what's wrong. Using the information from the QEMU arguments part of the log, the problem could be determined as a bug in the OpenGL 3D acceleration.
