---
layout: default
title: Classic Windows
parent: Guides
---

{% include toc.md %}

## Instructions

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Emulate".
3. Select "Windows".
4. Pick from the list of supported machines. See the [section below]({% link guides/classic-windows.md %}#compatibility) on compatibility for more information. Optionally change the amount of memory and CPU cores allocated to the machine and press "Continue".
5. Select the type of boot device (CD or floppy) and browse for the boot image. Some Windows installs (e.g. Windows 95) will boot from a floppy and run the setup from a CD. In those cases, choose floppy and select the boot IMG.
6. Press "Continue".
7. Specify the maximum amount of drive space to allocate. Press "Continue".
8. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools. Note: Older versions of Windows do not support SPICE tools and cannot access the shared directory. Press "Continue".
9. Press "Save" to create the VM. If you are installing a version of Windows that boots from a floppy and installs from a CD, select the installer ISO from the VM details screen. Press the Run button to start the VM.

## Compatibility

UTM provides two preset machine configurations for classic PC emulation.

### Intel i440FX based PC
This emulates a PC from around the year ~1996 and can be used to run any version of Windows before Windows XP. It is a 32-bit only machine with primary input handled through the PS/2 ports for maximum compatibility with earlier operating systems. Mouse input will only work in capture mode and USB 2.0 is supported (if the guest has the right drivers installed).

### Intel ICH9 based PC
This emulates a PC from around the year ~2009 and can be used to run Windows XP or higher. It is a 64-bit machine (compatible with 32-bit operating systems) and input is handed through USB HID devices. This machine can also support UEFI boot which is required by newer versions of Windows.

## Troubleshooting

### Mouse does not work
Older versions of Windows only support the emulated PS/2 input devices and require input capturing. On macOS, press Ctrl+Option or use the mouse icon on the toolbar to initiate input capture.

### Networking issues
To get networking working, you need to install the NE2000 compatible network drivers. [This page](https://wiki.qemu.org/Documentation/GuestOperatingSystems/Windows95#Networking) has an excellent guide on getting networking to work on Windows 95. For Windows 98 SE, the installer should automatically install the driver. If you are prompted to enter the IRQ number, make sure to use `09`.

### Windows 95: Windows Protection Error
You install to follow the instructions for [FIX95CPU](https://archive.org/details/fix-95-cpu-v3-final) in order to properly install Windows 95.

### Windows 98: Bypass modem setup
Follow [this guide](https://superuser.com/a/1762429) to bypass modem setup and connect directly to LAN.
