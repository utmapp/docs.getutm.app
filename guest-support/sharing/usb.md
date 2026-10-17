---
layout: default
title: USB
parent: Sharing
grand_parent: Guest Support
---
{% include toc.md %}

USB sharing allow you to connect a USB device to a virtual machine. It is supported by the QEMU backend and **macOS 27+**{: .label .label-green } the Apple backend.

**iOS**{: .label .label-blue } Only jailbroken or exploit-based installs of UTM support USB sharing. UTM SE does not support USB sharing.

## QEMU Backend

{: .note }
Due to the way macOS/iOS handles USB capturing (without custom kernel drivers), it is not possible to get a proper hardware reset on the connected device. The device will always be configured on the host before a software reset is sent to the device and it is seen by the virtual machine. This means that many devices will not work properly when captured by the virtual machine.

{: .note }
Some devices cannot be captured including built-in Apple webcams and **iOS**{: .label .label-blue } some external flash drives.

### Enabling USB Sharing

In the virtual machine configuration, make sure that ["USB sharing"]({% link settings-qemu/input.md %}#usb-sharing) is enabled.

Once the virtual machine is started, plug in the device and you should see a prompt to attach the device. You can also press the USB button on the [toolbar]({% link basics/controls.md %}) to see a list of devices which you can attach or detach.

{: .note }
**iOS**{: .label .label-blue } You will need a "Lightning to USB 3 Camera Adapter" on Lightning port devices.

## **macOS 27+**{: .label .label-green } Apple Backend

On macOS 27 and higher, USB devices can be passed through to Apple Virtualization virtual machines. macOS requires you to assign each device to UTM before UTM can see it.

1. Start the virtual machine.
2. Click the "Virtual Machine Accessories" item in the menu bar and assign the device to UTM. If only one virtual machine is running (or if its window is in front), the device will be connected to it automatically.
3. To connect or disconnect a device later, press the USB button on the [toolbar]({% link basics/controls.md %}) and select the device. Devices that are not assigned to UTM will not be listed.

A device can only be connected to one virtual machine at a time. If you connect a device that is in use by another virtual machine, UTM will ask you to confirm before moving it.

{: .note }
Some devices are not supported by Apple Virtualization and UTM will show an error explaining that the device cannot be captured.
