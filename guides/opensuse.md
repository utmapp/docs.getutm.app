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

## Finishing Installation

For the most part, everything should be up to date and running depending on your version. That said, it is always smart to ensure things are updated [using YaST](https://en.opensuse.org/YaST_Online_Update) or by running

```sh
sudo zypper up
```

## Enable clipboard and directory sharing

[Follow the instructions in this page.]({% link guest-support/linux.md %})
