---
layout: default
title: Windows 11
parent: Guides
---
{: .label .label-green }
**macOS**

{% include toc.md %}

This guide will help you create an Windows 10 or Windows 11 virtual machine from a fresh install.

## Downloads

* [UUP dump (Windows 10 21H2)](https://uupdump.net/known.php?q=21390)
* [UUP dump (Windows 11 21H2)](https://uupdump.net/known.php?q=22000.1098)
* [UUP dump (Windows 11 22H2)](https://uupdump.net/known.php?q=22621.674)

{: .warning }
Windows 11 22H2 or later requires using Windows 10, version 2004 or later for the ISO to be properly created. The current script for macOS will output a broken ISO. If you do not have a Windows computer, you can install an older version of Windows in UTM first and use that to create an ISO for a newer version.


## Instructions

1. Find the edition of Windows you want to install on [UUP dump](https://uupdump.net). Once you downloaded and extracted the installer creator, you need to run `uup_download_macos.sh` from Terminal to generate the ISO. (Read ["troubleshooting"](#cannot-run-uup_download_macossh) if you are having issues here.)

{: .note }
Make sure you select **arm64** if you are on Apple Silicon and **amd64** if you are on Intel!

{: style="counter-reset:none" }
2. Open UTM and click the "+" button to open the VM creation wizard.
3. Select "Virtualize".
4. Select "Windows".
5. Make sure "Import VHDX Image" is *unchecked* and "Install Windows 10 or higher" is *checked*. Also make sure "Install drivers and SPICE tools" is *checked*. Press "Browse" and select the ISO you built in step 1.
6. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
7. Specify the maximum amount of drive space to allocate. Press "Next" to continue.
8. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
9. Press "Save" to create the VM. Wait for the guest tools to finish downloading and press the Run button to start the VM.
10. Follow the Windows installer. If you have issues with the mouse, press the mouse capture button in the toolbar to send mouse input directly. Press Control+Option together to exit mouse capture mode. Sometimes, due to driver issues, you can enter and exit capture mode and the mouse cursor works normally again.

### Installing the Microsoft Store and UWP apps (optional)

{: .label .label-yellow }
**WIP**
1. Google the UWP apps (or any other apps available in the Microsoft Store) of interest to find its official download link from Microsoft.
    a. For example, if you wanted to download Windows Photo app, the following link is what you're looking for:
        https://apps.microsoft.com/store/detail/microsoft-photos/9WZDNCRFJBH4?hl=en-us&gl=us
2. Navigate to the [Online link generator for Microsoft Store](https://store.rg-adguard.net/), input your link in the searchbox, and click on the checkbox.
    a. The site will provide \*.appx dependencies needed for your app work.
3. Download all the \*.appx files corresponding to your Windows architecture along with the .Msixbundle file associated with your app.
    a. For example, if you want to install the Photos app on Windows 11 arm64, you would need to download these files:
      -Microsoft.NET.Native.Framework...arm64...appx
      -Microsoft.NET.Native.Runtime...arm64...appx
      -Microsoft.Services.Store.Engagement...arm64...appx
      -Microsoft.UI.Xaml.(2.0/2.1/2.2.4/2.7)...arm64...appx
      -Microsoft.VCLibs.140.00.UWPDesktop...arm64...appx
      -Microsoft.VCLibs.140.00...arm64...appx
      -Microsoft.Windows.Photos...neutral...msixbundle
4. Install .appx files with Windows PowerShell using the following command:
    `Add-AppPackage -Path .\[Location of the downloaded .appx file].appx`
5. After installing all the .appx dependencies, install the .Msixbundle using the same command.
    `Add-AppPackage -Path .\[Location of the downloaded .Msixbundle file].Msixbundle`
    
The app should be functional after completing the aforementioned steps. 
Check [this issue](https://github.com/utmapp/UTM/issues/3884) for more information.

## Troubleshooting

### Cannot run `uup_download_macos.sh`

In Terminal, go to the directory containing `uup_download_macos.sh`

```
$ cd path/to/extracted/files
```

Make sure that `uup_download_macos.sh` is executable by running

```
$ chmod +x uup_download_macos.sh
```

Make sure you have the prerequisites installed

```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
$ brew tap sidneys/homebrew
$ brew install aria2 cabextract wimlib cdrtools sidneys/homebrew/chntpw
```

Then you can run `uup_download_macos.sh`

```
$ ./uup_download_macos.sh
```

### Boots into EFI shell instead of Windows installer

Make sure you generated the right ISO for your architecture. Note that **arm64** is for Apple Silicon and **amd64** is for Intel.

### Installer crashes with BSOD `SYSTEM_THREAD_EXCEPTION_NOT_HANDLED`

You are using a version of Windows that is too old. The build number should be 21390 or higher.

### "This PC can't run Windows 11"

If you get this message trying to install Windows 11, you can bypass it with the following steps:

1. Press **Shift+F10** to open Command Prompt and type in `regedit.exe` to launch Registry Editor.
2. Navigate to **HKEY_LOCAL_MACHINE\SYSTEM\Setup**
3. Right click on the **Setup** key on the left size and choose New -> Key.
4. Create a key named `LabConfig`
5. Select the **LabConfig** key.
6. Create two new values: Choose New -> DWORD (32-bit) and create `BypassTPMCheck` and `BypassSecureBootCheck`. Set both values to 1.
7. Close out of Registry Editor and Command Prompt.
8. In setup, press the back button and then Next to continue installation.

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
