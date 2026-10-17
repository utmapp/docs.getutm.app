---
layout: default
title: Settings (Apple)
nav_order: 5
has_children: true
---
{: .label .label-green }
**macOS**

Apple Virtualization backend supports only virtualization and is less mature than QEMU. It is the only way to run macOS virtualized on Apple Silicon.

Some features of Apple Virtualization backend VMs are not part of the VM settings:

* **macOS 15+**{: .label .label-green } Removable drives can be changed from the VM window's toolbar while the VM is running.
* **macOS 27+**{: .label .label-green } [USB devices]({% link guest-support/sharing/usb.md %}) can be passed through from the VM window's toolbar.
* **macOS 27+**{: .label .label-green } The VM can be [run without saving changes]({% link advanced/disposable.md %}).
