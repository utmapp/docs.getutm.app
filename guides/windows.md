---
layout: default
title: Windows 11
parent: Guides
---
{: .label .label-green }
**macOS**

{% include toc.md %}

This guide will help you create a Windows 11 virtual machine from a fresh install.

## CrystalFetch

The easiest way to obtain a Windows installer ISO is with CrystalFetch on macOS, a free utility based off of [UUPDump](https://uupdump.net).

[ Download on the App Store](https://apps.apple.com/app/crystalfetch-iso-downloader/id6454431289){: .btn .btn-green }
[Download from GitHub](https://github.com/TuringSoftware/CrystalFetch/releases/latest/download/CrystalFetch.dmg){: .btn .btn-green }

By default, the latest release or release preview build for the host architecture will be selected. You can change the filter to include pre-release builds as well as server builds. You can collapse the current architecture to find builds for other architectures (i.e. for emulation).

## Instructions

1. Use CrystalFetch to download the latest installer ISO.
2. Open UTM and click the "+" button to open the VM creation wizard.
3. Select "Virtualize".
4. Select "Windows".
5. Make sure "Import VHDX Image" is *unchecked* and "Install Windows 10 or higher" is *checked*. Also make sure "Install drivers and SPICE tools" is *checked*. Press "Browse" and select the ISO you built in step 1.
6. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
7. Specify the maximum amount of drive space to allocate. Press "Next" to continue.
8. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
9. Press "Save" to create the VM. Wait for the guest tools to finish downloading and press the Run button to start the VM.
10. Press any key to start the Windows installer and follow the instructions on screen. If you have issues with the mouse, press the mouse capture button in the toolbar to send mouse input directly. Press Control+Option together to exit mouse capture mode. Sometimes, due to driver issues, you can enter and exit capture mode and the mouse cursor works normally again.

### Installing the Microsoft Store and UWP apps (optional)

{: .label .label-yellow }
**WIP**

On the latest pre-release builds the Microsoft Store should be installed automatically. Older versions can follow [this guide](https://dabigblob.github.io/ms-store-arm64/) or check [this issue](https://github.com/utmapp/UTM/issues/3884) for more information.

## Troubleshooting

### Boots into EFI shell instead of Windows installer

First, make sure that you pressed any key during boot to enter the installer. Also, make sure you generated the right ISO for your architecture. Note that **arm64** is for Apple Silicon and **amd64** is for Intel.

### Installer crashes with BSOD `SYSTEM_THREAD_EXCEPTION_NOT_HANDLED`

You are using a version of Windows that is too old. The build number should be 21390 or higher.

### "This PC can't run Windows 11"

If you get this message trying to install Windows 11, there can be a number of possible reasons.

#### Secure Boot

On newer versions of UTM, Secure Boot and TPM should be enabled automatically. You can also enable it manually in Settings under [QEMU]({% link settings-qemu/qemu.md %}#tpm-20-device). If you are on an older version of UTM, you can disable the checks in the Windows installer:

1. Press **Shift+F10** to open Command Prompt and type in `regedit.exe` to launch Registry Editor.
2. Navigate to **HKEY_LOCAL_MACHINE\SYSTEM\Setup**
3. Right click on the **Setup** key on the left size and choose New -> Key.
4. Create a key named `LabConfig`
5. Select the **LabConfig** key.
6. Create two new values: Choose New -> DWORD (32-bit) and create `BypassTPMCheck` and `BypassSecureBootCheck`. Set both values to 1.
7. Close out of Registry Editor and Command Prompt.
8. In setup, press the back button and then Next to continue installation.

#### Core count

Windows require at least 2 cores to install. If you are installing x86_64 Windows on an Intel Mac or ARM64 Windows on an Apple Silicon Mac, the default setting will be to use the number of cores on your system. However, if you are installing x86_64 Windows on an Apple Silicon Mac, the default setting is to use only a single core. This is because due to memory ordering requirements, emulating multiple x86_64 cores on an ARM64 system will be done on a single core and thus reduce performance.

At the cost of correctness, you can force multiple cores by going to the [System]({% link settings-qemu/system.md %}#cpu) settings and changing the number of cores to 2 or higher and checking "Force multicore." Note that you may occasionally experience odd crashes as a result of this.

### Ping does not work

Note that due to libslirp limitations, `ping` will not work and so Windows may think that there is still no internet connection.

### Networking does not work

Make sure you installed the SPICE guest tools, which includes the network drivers.

If Windows 11 setup is stuck due to lack of network connection:

1. Go to the language select screen (you may need to restart the setup if you are past this screen).
2. Press **Shift + F10** to launch Command Prompt.
3. Type in `OOBE\BYPASSNRO` and press Enter.
4. Your VM should reboot and at the setup screen you should see an option for "I don't have internet."
5. Once Windows setup is completed, make sure to install the SPICE guest tools for network drivers.

### SPICE tools did not install automatically

See [this page]({% link guest-support/windows.md %}#windows-xp-and-higher) for more details.

### "Why did my PC restart" blue screen

This is likely due to using the "Shared" network mode[^1]. If so, try switching to a "Bridged" network mode instead.

1. Edit Virtual Machine
2. Under "Devices" select "Networks"
3. If the "Network Mode" is `Shared Network` select `Bridged (Advanced)` instead

[^1]: https://github.com/utmapp/UTM/issues/3411
