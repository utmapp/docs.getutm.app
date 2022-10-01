---
layout: default
title: USB
parent: Sharing
grand_parent: Guest Support
---
USB sharing allow you to connect a USB device to a virtual machine. It is supported only by the QEMU backend.

**iOS**{: .label .label-blue } Only jailbroken or exploit-based installs of UTM support USB sharing. UTM SE does not support USB sharing.

{: .note }
Due to the way macOS/iOS handles USB capturing (without custom kernel drivers), it is not possible to get a proper hardware reset on the connected device. The device will always be configured on the host before a software reset is sent to the device and it is seen by the virtual machine. This means that many devices will not work properly when captured by the virtual machine.

{: .note }
Some devices cannot be captured including built-in Apple webcams and **iOS**{: .label .label-blue } some external flash drives.

## Enabling USB Sharing

In the virtual machine configuration, make sure that ["USB sharing"]({% link settings-qemu/input.md %}#usb-sharing) is enabled.

Once the virtual machine is started, plug in the device and you should see a prompt to attach the device. You can also press the USB button on the [toolbar]({% link basics/controls.md %}) to see a list of devices which you can attach or detach.

{: .note }
**iOS**{: .label .label-blue } You will need a "Lightning to USB 3 Camera Adapter" on Lightning port devices.
