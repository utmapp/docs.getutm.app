---
layout: default
title: Virtualization
parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Balloon Device
The balloon device allows the guest operating system (with supported drivers) to more intelligently request RAM from the host. This is highly recommended.

## Entropy Device
The entropy device is used by supported guest operating systems for cryptographic tasks.

## **macOS 12+**{: .label .label-green } Sound
Sound support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI.

## **macOS 12+**{: .label .label-green } Keyboard
Keyboard support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI.

## **macOS 12+**{: .label .label-green } Pointer
Pointer support for macOS or **macOS 13+**{: .label .label-green } Linux booting from UEFI.

## **macOS 13+**{: .label .label-green } Trackpad

Emulates a trackpad for macOS guests. Requires Ventura or higher guest. This allows support for trackpad gestures.

## **macOS 13+**{: .label .label-green } Rosetta
See [Rosetta]({% link advanced/rosetta.md %}) for more details.

## **macOS 13+**{: .label .label-green } Clipboard Sharing
On Linux guests booting from UEFI, install `spice-vdagent` to enable clipboard sharing.
