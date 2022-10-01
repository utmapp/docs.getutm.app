---
layout: default
title: Headless
parent: Advanced
---
Headless mode allows you to run a virtual machine in the background.

{: .note }
UTM needs to be open while the headless virtual machine is running.

To setup headless mode, open the virtual machine configuration and [delete any display device]({% link settings-qemu/devices/devices.md %}) as well as any serial device that is set to "Built-in Terminal" mode. It is highly recommended that you set up at least one serial device in one of the other modes so that you can communicate with the virtual machine. See [this page]({% link advanced/serial.md %}) for more details.
