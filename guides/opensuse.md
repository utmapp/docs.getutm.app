---
layout: default
title: openSUSE
parent: Guides
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Downloads

* [openSUSE Tumbleweed](https://get.opensuse.org/tumbleweed/)
* [openSUSE Leap](https://get.opensuse.org/leap)
* [openSUSE MicroOS](https://get.opensuse.org/microos/#download)
* [openSUSE Leap Micro](https://get.opensuse.org/leapmicro)


## Creating a new virtual machine

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Linux".
4. Click "Browse" and select the openSUSE ISO downloaded from the links above. Press "Continue" to continue.
5. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Continue" to continue.
6. Specify the maximum amount of drive space to allocate. Press "Continue" to continue.
6. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Continue" to continue.
8. Press "Save" to create the VM and press the Run button to start the VM.
9. Go through the Ubuntu installer. If the reboot fails, you can manually quit the VM, unmount the installer ISO, and start the VM again to boot into your new installation.

## Installing Ubuntu Desktop

If you installed Ubuntu Server, then at the end of the installation, you will not have any GUI. To install Ubuntu Desktop, log in and run:

```
$ sudo apt update
$ sudo apt install ubuntu-desktop
$ sudo reboot
```

## Enable clipboard and directory sharing

[Follow the instructions in this page.]({% link guest-support/linux.md %})

## Troubleshooting

### Cannot boot into installer

If you start the VM and are stuck at the EFI screen (`BdsDxe: failed to load Boot0001` or `UEFI Interactive Shell`), try the following in order.

1. Make sure you have the installer ISO selected. Click the disk icon on the toolbar and check that there is a menu option for `CD/DVD (ISO) Image (usb): ubuntu-xxx.iso`. If it says `CD/DVD (ISO) Image (usb): none`, then highlight that menu and choose `Change` and then select the ISO. If you don't have any selectable menu option, follow the guide again and make sure you have added a removable drive. Then restart the VM.
2. Next, try to get into the EFI Shell. If you see `UEFI Interactive Shell` then you are already in the shell. Otherwise, restart the VM and quickly press the Esc key to enter the shell.
3. In the EFI shell make sure you see `FS0: Alias(s):CD0h0a0a::BLK1:` near the top or something similar. If not, then double check your configuration and make sure you have a removable drive configured and the installer ISO mounted. Also check that your ISO is valid.
4. Type in: `fs0:\efi\boot\bootaa64.efi` and you should see GRUB. Then select `Ubuntu Server` to continue with the install.

### Networking is unavailable

If the hardware enumeration order changes, your network settings may need to be updated.

1. Run `ip link show` and look at the last adapter name. For example, it may be listed as `enp0s1`.
2. Edit `/etc/netplan/00-installer-config.yaml` and copy your configuration for `enp0s8` (or whatever the old adapter was named) and paste it immediately after for `enp0s1` (or whatever the new adapter is named).
3. Reboot and you should be able to use networking again.
