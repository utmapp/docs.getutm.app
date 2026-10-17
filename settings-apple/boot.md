---
layout: default
title: Boot
parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Operating System
macOS and Linux are supported. macOS guests can only run on Apple Silicon.

## Bootloader
This be the same as the operating system (macOS/Linux) to use the default boot loader. **macOS 13+**{: .label .label-green } UEFI bootloader must be used to boot Linux with graphics support.

## **macOS 27+**{: .label .label-green } Secure Boot
Only available for Linux guests booting from UEFI. If enabled, only operating systems signed by Microsoft or a trusted vendor will boot. Most major Linux distributions are supported. The Secure Boot state is stored in the VM's EFI variables and is updated when the settings are saved. Disabling UEFI boot will also disable Secure Boot.

## Linux Settings
Only applicable when UEFI boot is not used.

### Kernel Image
Select an **uncompressed** Linux kernel to boot from.

### Ramdisk
Optionally select an initial ramdisk.

### Boot arguments
The kernel boot arguments. `console=hvc0 root=/dev/vda` is highly recommended.

## macOS Settings

### IPSW Install Image
Pass in an universal macOS IPSW to install.
