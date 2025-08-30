---
layout: default
title: Clipboard
parent: Sharing
grand_parent: Guest Support
---
{% include toc.md %}

Clipboard sharing allows the guest and host to share clipboard contents. It is supported by the QEMU backend.

**macOS 13+**{: .label .label-green } Clipboard sharing is now supported for Linux guests running on the Apple backend. For macOS guests, sharing is supported when both the guest and host are running macOS 15 or higher and [macOS]({% link guest-support/macos.md %}) guest tool is running.

## Enabling Clipboard Sharing

1. In the virtual machine configuration, make sure that "Clipboard sharing" is enabled for [QEMU]({% link settings-qemu/sharing.md %}#clipboard-sharing) or [Apple]({% link settings-apple/virtualization.md %}#macos-13-clipboard-sharing) backend.
2. Install the guest tools on [Linux]({% link guest-support/linux.md %}) or [Windows]({% link guest-support/windows.md %}).
3. Reboot the virtual machine.
