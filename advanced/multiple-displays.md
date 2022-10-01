---
layout: default
title: Multiple Displays
parent: Advanced
---
You can configure a virtual machine with multiple display devices or "built in terminal" mode serial devices.

**macOS**{: .label .label-green } Apple backend (macOS guests) does not support multiple graphical displays.

To setup multiple displays, open the virtual machine configuration and [add a new display or serial device]({% link settings-qemu/devices/devices.md %}). In case of a serial device, choose "Built-in Terminal" mode.

When creating new display devices, it is recommended that you use `virtio-gpu-pci` or `virtio-gpu-gl-pci` or `secondary-vga` as some of the other display hardware are designed to only work as the primary video device.

{: .label .label-green }
**macOS**

On macOS, when you start the virtual machine, a new window is created for each additional display and terminal. If you close a window, you can re-open it from the [toolbar]({% link basics/controls.md %}) by clicking the display icon.

{: .label .label-blue }
**iOS**

On iOS, you can switch the output device from the [toolbar]({% link basics/controls.md %}) by clicking the display icon. If you use AirPlay or attach to an external display, you can control the output of that display from the same menu.

On iPadOS, you can create a new window from the same toolbar entry. Each new window can be set to output a different display or to mirror the same display.
