---
layout: default
title: Serial
parent: Advanced
---
{% include toc.md %}

UTM supports serial device emulation through network sockets (QEMU backend only) or pseudo-TTY device. To setup, add a new serial device ([QEMU]({% link settings-qemu/devices/devices.md %}) or **macOS**{: .label .label-green } [Apple]({% link settings-apple/devices/devices.md %})).

When the virtual machine is started, any serial device (excluding built-in terminal) will be listed in the [details]({% link basics/basics.md %}) and you can use this path to connect to the port.

## **macOS**{: .label .label-green } Pseudo-TTY

The easiest way to connect to a PTTY device is with the `screen` command:

```
$ screen /dev/ttys006
```

In this example the PTTY device was created at `/dev/ttys006`.
