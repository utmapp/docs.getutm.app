---
layout: default
title: Classic Mac OS
parent: Guides
---

{% include toc.md %}

UTM currently supports emulating the following classic Machintosh:
* Macintosh Quadra 800 (1993, M68K)
* Power Macintosh G4 (1999, PPC)

## Instructions

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Emulate".
3. Select "Classic Mac OS".
4. Pick from the list of supported machines. See the table below for the Mac OS versions that each machine supports. Optionally change the amount of memory allocated to the machine and press "Continue".
5. Select the boot ISO image for the Mac OS installer. You can dump the installer CD or obtain it through other means.
6. If the machine you selected requires a ROM, you must provide it at this screen. You can obtain the ROM from a physical Machintosh or through other means.
7. Press "Continue".
8. Specify the maximum amount of drive space to allocate. Press "Continue".
9. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. Press "Continue".
10. Press "Save" to create the VM. Press the Run button to start the VM.

## Installation

1. Boot the installer disk.
2. Launch "Drive Setup" (typically found in the "Utilities" directory of the installer CD)
3. Select the hard drive and initialize it.
4. Quit "Drive Setup".
5. Launch the installer from the CD.
6. Follow the wizard up to the last step (before "Start").
7. Press "Options" and uncheck "Update Apple Hard Disk Drivers".
8. Press "Start" to install Mac OS.

## Compatibility

| Machine    | Architecture | Operating System | PMU Setting | Notes                                                     |
|------------|--------------|------------------|-------------|-----------------------------------------------------------|
| Quadra 800 | m68k         | Mac OS 7.1       |             |                                                           |
| Quadra 800 | m68k         | Mac OS 7.5       |             |                                                           |
| Quadra 800 | m68k         | Mac OS 8.1       |             |                                                           |
| G4         | ppc          | Mac OS 9.0       | PMU-ADB     | Requires rom version 5.2.1 or above, mouse wiggle to boot |
| G4         | ppc          | Mac OS 9.1       | PMU         |                                                           |
| G4         | ppc          | Mac OS 9.2       | PMU         |                                                           |
| G4         | ppc          | Mac OSX 10.0     | PMU-ADB     | Audio crackle, channel issue                              |
| G4         | ppc          | Mac OSX 10.1     | PMU-ADB     | Audio channel issue                                       |
| G4         | ppc          | Mac OSX 10.3     | PMU         | Audio has speed drift                                     |
| G4         | ppc          | Mac OSX 10.4     | PMU         |                                                           |
| G4         | ppc          | Mac OSX 10.5     | PMU         |                                                           |

The information is derived from [this page for QEMU m68k](https://www.emaculation.com/doku.php/m68k-qemu-on-osx) and [this page for QEMU ppc](https://www.emaculation.com/doku.php/ppc-osx-on-qemu-for-osx).

## Troubleshooting

### Boot gets stuck with a question mark (M68K) or OpenBIOS (PPC)
There are many broken Mac OS installer ISOs floating around on the internet. Make sure the installer ISO you have is known to be working.

### Installer gets stuck for a very long time
Make sure you unchecked "Update Apple Hard Disk Drivers" from "Options" before starting the install. If it still gets stuck, reset the VM and try again. Note that sometimes, you might have to wait upwards of an hour for the install to finish.

### (PPC) Startup crashes with "illegal exception" or hang while loading
There are some known instability with the Screamer audio device. If you restart the VM a couple of time, it should work. You can also disable audio and improve stability by going into the VM settings and deleting the Sound device.
