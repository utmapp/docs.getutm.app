---
layout: default
title: Windows
parent: Guest Support
---
{% include toc.md %}

In order to use all the features of UTM, you should install the Windows Guest Tools in the virtual machine guest. The tools support Windows XP or higher on x86_64 (excluding Windows XP), i386, and arm64 builds.

## Installation

### Windows 10 and higher
If the guest tools ISO is mounted on a second CD drive, then it can be installed automatically during Windows Setup.
1. In the UTM new virtual machine wizard, make sure to select "Windows"
2. Check "Install Windows 10 or higher"
3. Check "Install drivers and SPICE tools"

Once the wizard completes, the Windows Guest Tools will download automatically and it will be mounted to the newly created virtual machine. Wait until the download completes and start the virtual machine. After finishing the installation, all drivers and the guest tools will be installed.

### Windows XP and higher
If you are running an older version of Windows or if you have already completed Windows Setup, you can install the guest tools manually.

{: .label .label-blue }
**iOS**
1. [Open the action menu]({% link basics/actions.md %}) and select "Install Windows Guest Tools..."
2. Wait for the tools to finish downloading and it should be automatically mounted on the last removable drive.
3. Start the virtual machine.

{: .label .label-green }
**macOS**
1. Start the virtual machine.
2. [On the toolbar click the CD icon]({% link basics/controls.md %}) and select "Install Windows Guest Tools..."
3. Wait for the tools to finish downloading and it should be automatically mounted on the last removable drive.

{: style="counter-reset:none" }
4. Once Windows starts up and you are logged in, open "My Computer" and find the CD drive labeled "UTM".
5. Launch `spice-guest-tools-xxx.exe` where `xxx` is the version number.
6. Follow the setup wizard to install the guest tools.

## Download
You can manually download the guest tools ISO [here][1].

## SPICE WebDAV
If [QEMU SPICE WebDAV directory sharing]({% link settings-qemu/sharing.md %}#spice-webdav) is enabled, you can access it from "My Computer" as a network drive.

If you do not see the network drive, run `C:\Program File\SPICE webdavd\map-drive.bat`.

[1]: https://getutm.app/downloads/utm-guest-tools-latest.iso
