---
layout: default
title: Virtualization
parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Balloon Device
Only available for Linux guests. The balloon device allows the guest operating system (with supported drivers) to more intelligently request RAM from the host. This is highly recommended.

## Entropy Device
The entropy device is used by supported guest operating systems for cryptographic tasks.

## Sound
Sound support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI. Input (microphone) and output (speakers) can be enabled separately.

* **Disabled** No sound device.
* **Input Only** Only the host microphone is passed to the guest.
* **Output Only** Only guest audio is played on the host. Since the microphone is not used, Bluetooth headphones will not switch to the lower quality headset mode.
* **Input and Output** Both the microphone and speakers are available to the guest.

## Keyboard
Keyboard support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI.

* **Disabled** No keyboard device.
* **Generic USB** A generic USB keyboard.
* **Mac Keyboard (macOS 14+)** Emulates a Mac keyboard for macOS guests (requires Sonoma or higher host and guest). On other guests, a generic USB keyboard is used.

## Pointer
Pointer support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI.

* **Disabled** No pointing device.
* **Generic Mouse** A generic USB pointing device.
* **Mac Trackpad (macOS 13+)** Emulates a trackpad for macOS guests (requires Ventura or higher host and guest). This allows support for trackpad gestures. On other guests, a generic mouse is used.

## **macOS 13+**{: .label .label-green } Rosetta
See [Rosetta]({% link advanced/rosetta.md %}) for more details.

## **macOS 13+**{: .label .label-green } Clipboard Sharing
On Linux guests booting from UEFI, install `spice-vdagent` to enable clipboard sharing.
