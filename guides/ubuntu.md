---
layout: default
title: Ubuntu
parent: Guides
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Downloads

* [Ubuntu Server for ARM](https://ubuntu.com/download/server/arm)
* [Ubuntu Desktop for Intel](https://ubuntu.com/download/desktop)

## Creating a new virtual machine

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Linux".
4. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Continue" to continue.
5. Click "Browse" and select the Ubuntu Server ISO downloaded from the link above. Press "Continue" to continue.
6. Specify the maximum amount of drive space to allocate. Press "Continue" to continue.
7. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Continue" to continue.
8. Press "Save" to create the VM and press the Run button to start the VM.
9. Go through the Ubuntu installer. At the end, you'll have the option to "Reboot Now," but after selecting that option and rebooting, the reboot will fail. (It will hang at a black screen with a blinking cursor.) This is expected!
10. Manually quit the VM, unmount the installer ISO, and start the VM again to boot into your new installation.

## Installing Ubuntu Desktop

If you installed Ubuntu Server, then at the end of the installation, you will not have any GUI. To install Ubuntu Desktop, log in and run:

```
$ sudo apt update
$ sudo apt install ubuntu-desktop
$ sudo reboot
```

## Enable clipboard and directory sharing

[Follow the instructions in this page.]({% link guest-support/linux.md %})

## Installing Rosetta
First install `binfmt-support`.

```
$ sudo apt install binfmt-support
```

Then, follow [this guide]({% link advanced/rosetta.md %}) to install Rosetta.

## Installing x86_64 Multiarch
For Rosetta to work, you will have to enable x86_64 packages.
For Ubuntu versions from 24.04 onwards using the package manager `apt`, can be updated by adding the archiectrure to your source list `/etc/apt/sources.list.d/` using the `deb822` format. For example on Ubuntu:

```
Types: deb
URIs: http://ports.ubuntu.com/ubuntu-ports/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
Architectures: arm64

Types: deb
URIs: https://security.ports.ubuntu.com/ubuntu-ports/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
Architectures: arm64

Types: deb
URIs: http://us.archive.ubuntu.com/ubuntu/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
Architectures: amd64

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
Architectures: amd64
```

> **⚠️ WARNING: Multi-Arch Hazard on Ubuntu**
> 
> Running `sudo dpkg --add-architecture amd64` on Ubuntu assumes that the update
> binary URLs are identical across architectures. **They are not** — Ubuntu’s mirrors use architecture-specific paths.
> If this command breaks apt, make sure architecture-specific repository lines exist for both the `arm64` and `amd64` sources.

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

### Black screen during boot
On ARM64 it has been reported that doing this may enable two wait services: NetworkManager-wait-online.service and systemd-networkd-wait-online.service that causes a black screen at boot.
To verify the fix is needed one can run:

```bash
systemctl is-enabled NetworkManager-wait-online.service systemd-networkd-wait-online.service
```

If you see two lines showing 'enabled' instead of one, the one that should be disabled can be done like:
```bash
systemctl disable systemd-networkd.service
```

You can create a serial device in the VM settings to access the command line and run the commands if nothing shows up on screen.
