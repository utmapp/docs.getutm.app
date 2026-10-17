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

## DirectX Graphics
**WIP**{: .label .label-yellow }

Windows 11 guests running in the QEMU backend can use accelerated DirectX graphics with an experimental 3D graphics driver included in the guest tools. Game compatibility is currently limited and the driver may cause instability in the guest.

### Requirements
* **macOS 13+**{: .label .label-green } or **iOS 16+**{: .label .label-blue }
* A GPU accelerated [display card]({% link settings-qemu/devices/display.md %}#emulated-display-card) (one ending in `-gl`). The new VM wizard selects one by default for Windows.
* The "Renderer Backend" in [preferences]({% link preferences/preferences.md %}) must be "Default" or "ANGLE (Metal)" and the "DirectX Driver" must not be "Disabled". The Apple Core OpenGL backend does not support DirectX.

### Installation
We recommend installing the 3D graphics driver on a fresh install of Windows. During the installation of the guest tools, you will be prompted to select the experimental graphics driver.

{: .warning }
If Windows is already running the older display only driver, you must first run the uninstall script found on the guest tools ISO before installing the experimental graphics driver.

### DirectX Driver
The host side of DirectX rendering can use one of two drivers which can be selected in the [preferences]({% link preferences/macos.md %}#directx-driver):

* **DXMT** supports DirectX 11. This is the only driver available on iOS.
* **macOS 14+**{: .label .label-green } **D3DMetal** supports DirectX 12 (when available). On Apple Silicon, D3DMetal requires Rosetta to be installed.

By default, D3DMetal is used when it is available. If Rosetta is not installed on an Apple Silicon Mac, UTM falls back to DXMT.

## Download
You can manually download the guest tools ISO [here][1].

## SPICE WebDAV
If [QEMU SPICE WebDAV directory sharing]({% link settings-qemu/sharing.md %}#spice-webdav) is enabled, you can access it from "My Computer" as a network drive.

If you do not see the network drive, run `C:\Program Files\SPICE webdavd\map-drive.bat`.

[1]: https://getutm.app/downloads/utm-guest-tools-latest.iso
