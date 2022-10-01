---
layout: default
title: Dynamic Resolution
parent: Guest Support
---
{% include toc.md %}

Dynamic resolution allows the virtual machine to change resolution to match the current window size (including full screen window). It it only supported on QEMU backend virtual machines and requires guest tools to be installed.

## Enabling Dynamic Resolution

1. In the virtual machine configuration, make sure that ["Auto resolution"]({% link settings-qemu/devices/display.md %}#auto-resolution) is checked.
2. Install the guest tools on [Linux]({% link guest-support/linux.md %}) or [Windows]({% link guest-support/windows.md %}).
3. Reboot the virtual machine.

**macOS**{: .label .label-green } When you resize the virtual machine window, it should automatically request to the guest agent to change the resolution to match that size.

**iOS**{: .label .label-blue } When you change the display orientation, it will request the guest agent for a resolution change. On iPadOS, resolution change will also be requested for Split View, Slide Over, and window resizing in Stage Manager.

## Troubleshooting

### Resolution is not changing on Linux

There is a known bug on some distributions that prevents dynamic resolution from working. The following command will force the window manager to update the resolution:

```
$ xrandr --output Virtual-1 --auto
```
