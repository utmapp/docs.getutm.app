---
layout: default
title: Debian 11 + Rosetta
parent: Guides
---
{: .label .label-green }
**macOS 13+**

{: .highlight }
There is a bug present in Linux virtual machines on Ventura and the base M1 chip which causes the virtual machine to kernel panic and freeze up randomly. Unfortunately, this means that base M1 users should avoid Apple Virtualization backend until Apple or Linux maintainers provide a fix.

{% include toc.md %}

This page will guide you to installing Debian on your Apple Silicon Mac running macOS Ventura or higher with support for Rosetta for running Intel applications on Linux.

## Downloads
* [Debian Net Installer](https://cdimage.debian.org/debian-cd/current/arm64/iso-cd/)

## Creating a new virtual machine
1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Linux".
4. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Continue".
5. Check "Use Apple Virtualization" and "Enable Rosetta (x86_64 Emulation)"
6. Click "Browse" and select the Debian installer ISO from the link above. Press "Continue".
7. Specify the maximum amount of drive space to allocate. Press "Continue".
8. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Continue".
9. Press "Save" to create the VM and press the Run button to start the VM.
10. Select "Install" and follow through the setup wizard.

### Recommended Install Options
* Install to `Virtual disk 1 (vda)`, using entire disk, all files in one partition
* In "Software selection": check "GNOME", "SSH server", and "standard system utilities"

### Enabling sudo
After installing and logging in, you will find that the default user does not have `sudo` privileges. Open a terminal and use the following commands to enable it.

```
$ set USERNAME=`whoami`
$ su -p
# /usr/sbin/usermod -aG sudo $USERNAME
```

You will need to restart for the changes to take place.

## Shared Directory
Follow [this guide]({% link guest-support/linux.md %}#macos-virtiofs) to enable VirtioFS directory sharing. We recommend using `/media/share` as the mount point.

## Clipboard Sharing
Install `spice-vdagent` and reboot to enable clipboard sharing.

```
$ sudo apt install spice-vdagent
```

## Installing Rosetta
First install `binfmt-support`.

```
$ sudo apt install binfmt-support
```

Then, follow [this guide]({% link advanced/rosetta.md %}) to install Rosetta.

## Installing x86_64 Multiarch
For Rosetta to work, you will have to enable x86_64 packages.

```
$ sudo dpkg --add-architecture amd64
$ sudo apt update
```

You can now install and run any x86_64 package in the Debian repository with `sudo apt install packagename:amd64`.
