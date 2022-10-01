---
layout: default
title: Boot
parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Operating System
Currently only **macOS 12+**{: .label .label-green } macOS and Linux are supported.

## Bootloader
This be the same as the operating system (macOS/Linux) to use the default boot loader. **macOS 13+**{: .label .label-green } UEFI bootloader must be used to boot Linux with graphics support.

## Linux Settings

### Kernel Image
Select an **uncompressed** Linux kernel to boot from.

### Ramdisk
Optionally select an initial ramdisk.

### Boot arguments
The kernel boot arguments. `console=hvc0 root=/dev/vda` is highly recommended.

## **macOS 12+**{: .label .label-green } macOS Settings

### IPSW Install Image
Pass in an universal macOS IPSW to install.
