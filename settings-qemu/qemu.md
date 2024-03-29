---
layout: default
title: QEMU
parent: Settings (QEMU)
---
{% include toc.md %}

## Logging
When enabled, the standard output and error of QEMU will be redirected to a log file stored in the .utm bundle. This is useful for debugging issues as well as submitting bug reports. If the log file exists, you can also export it out of the .utm bundle.

{: .warning }
The debug log can contain personally identifying information including the names of mounted drives and key strokes. Make sure to check the contents before sharing the log with anyone.

## Tweaks
These are advanced options for tweaking QEMU. Most users do not need to change any of the defaults.

### UEFI Boot
Currently UEFI support is limited to i386, x86_64, arm, and aarch64 systems. Some operating systems such as older versions of Windows do not support booting from UEFI and this option can be disabled.

### RNG Device
This emulates a random number generator that can be used by the guest operating system for cryptographic tasks. Some guests do not work properly with QEMU's RNG device and this option can be disabled in those cases.

### Balloon Device
The balloon device allows the guest operating system (with supported drivers) to more intelligently request RAM from the host. This is highly recommended.

### TPM 2.0 Device
TPM 2.0 is required to install and update Windows 11. It can be used to protect data in the guest however in practice this claim is not widely agreed by security experts. When TPM 2.0 and UEFI are both enabled, UEFI Secure Boot support will also be available. However, to enable Secure Boot on an existing VM, it is necessary to enroll the UTM platform key. The easiest way to do this is to select the "Reset UEFI Variables" option under "Maintenance".

{: .warning }
Note that the host will always be able to read these secrets and therefore no expectation of physical security is provided.

### Use Hypervisor
When the [target architecture matches the host]({% link settings-qemu/system.md %}#architecture), you can use the hypervisor to enable virtualization. This allows the host to natively execute the guest instructions without having to re-compile and translate the code. If virtualization is not supported, this option does nothing and will fall back to emulation.

**iOS**{: .label .label-blue } This option is not supported on most installations. See [the install guide]({% link installation/ios.md %}) for more details.

### Use TSO
TSO (Total Store Ordering) is an Apple Silicon hardware feature that enhances performance of x86 emulators such as [FEX-Emu](https://github.com/FEX-Emu/FEX) on Apple Silicon. Note that it is recommended that TSO be disabled if you do not need to emulate x86 because it can reduce performance of other tasks. If this is enabled, be sure to disable software TSO in your emulator configuration. This option is only available when Hypervisor is enabled on Apple Silicon.

**iOS**{: .label .label-blue } This option is not supported on most installations. See [the install guide]({% link installation/ios.md %}) for more details.

**macOS**{: .label .label-green } This option is not supported on macOS however when using the Apple virtualization backend, [a similar option is available]({% link settings-apple/virtualization.md %}#macos-13-rosetta).

### Use local time for base clock
This specifies the `-rtc base=localtime` option in QEMU. This synchronizes the guest clock to the local clock without any offsets. On some Linux guests, the RTC base is expected to be UTC and so this option should be disabled.

### Force PS/2 controller
Only applicable to i386/x86_64 system guests. By default, the built-in PS/2 controller is disabled to prevent collision with the emulated USB input devices. However, some older operating systems do not support USB and so enabling this will allow input to be passed through the PS/2 device. When the PS/2 input is used, the only support mode of cursor input is **iOS**{: .label .label-blue } "drag cursor" or **macOS**{: .label .label-green } "capture cursor".

## Maintenance
These options are not saved in the configuration but only affect the next start of the VM. If UTM is quit before starting the VM, the change will not take place.

### Reset UEFI Variables
You can use this if your boot options are corrupted or if you wish to re-enroll in the default keys for secure boot.

## QEMU Machine Properties
For advanced users who wish to append additional `-machine` QEMU arguments. Note that default `-machine` properties are generated by UTM to work best with the guest system. When a custom machine property is specified, if it overlaps with one of the default properties, it will be overridden. Otherwise, it will be appended to the custom properties.

## QEMU Arguments
This area allows you to quickly see what QEMU arguments the UTM configuration resolves to. This is not recommended for typical users. When debugging UTM issues, it is often helpful to try to reproduce the issue in QEMU and the "export" action allows you to get a text dump of the arguments.

{: .note }
UTM uses a customized fork of QEMU and therefore not all arguments will be supported in a vanilla QEMU installation. Additionally, if you wish to run QEMU with the generated arguments, you may want to remove the SPICE arguments and replace it with a different frontend.

{: .note }
At the end of the argument list is the option to add additional QEMU arguments. You should use quotes to escape spaces in any additional argument. This option is provided only for debugging purposes and the functionality may change or be removed in the future.
