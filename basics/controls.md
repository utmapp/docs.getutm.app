---
layout: default
title: Controls
parent: Basics
nav_order: 2
---

{: .screenshots }
[![]({% link assets/images/macos-vm-toolbar.png %})]({% link assets/images/macos-vm-toolbar.png %})
[![]({% link assets/images/iphone-vm-toolbar.png %})]({% link assets/images/iphone-vm-toolbar.png %})

1. Power off the virtual machine. This will discard any unsaved data. It is recommended that you shut down the virtual machine from the guest operating system. **macOS**{: .label .label-green } You can long press on this button for additional power-down options:
    1. *Request power down*: Sends power down request to the guest. This simulates pressing the power button on a PC.
    2. *Force shut down*: Tells the VM process to shut down with risk of data corruption. This simulates holding down the power button on a PC. This is the default option.
    3. *Force kill*: Force kill the VM process with high risk of data corruption.
2. Suspend the virtual machine when supported.

{: .note }
The suspend feature will not work if any device that is in use does not support suspend. This typically includes emulated NVMe devices as well as GPU accelerated display cards. Additionally, QEMU hypervisor on Intel does not support suspend.

{: style="counter-reset:none" }
3. Reset the virtual machine. This will discard any unsaved data.
4. **macOS**{: .label .label-green } Capture the cursor and keyboard for exclusive use by the virtual machine. This allows certain key combinations such as Cmd+Tab to be sent to the virtual machine. Once captured, the [key combination Control+Option]({% link advanced/preferences/macos.md %}#use-commandoption-for-input-capturerelease) can be used to release the capture. The same key combination can also be used to enter capture mode as well.
5. **iOS**{: .label .label-blue } When in graphical display mode, the first press will lock the display to fit. That means whenever the resolution changes, the display will scale accordingly so the entire screen is used. A second press will release the lock and set the display scaling to 1x. When in terminal display mode, a press will send the [resize command]({% link settings-qemu/devices/serial.md %}#resize-console-command). **macOS**{: .label .label-green } This button is only enabled in terminal display mode and has the same behaviour as iOS.
6. USB devices that currently detected are listed and can be connected or disconnected. **iOS**{: .label .label-blue } Not all builds support this option. **macOS**{: .label .label-green } Apple virtualization backend does not support this option. If unsupported or if [USB sharing is disabled]({% link settings-qemu/input.md %}#usb-sharing), this button will be disabled or missing.
7. When one or more [removable drives]({% link settings-qemu/drive/drive.md %}) are configured, you can change the mounted image in this menu. **iOS**{: .label .label-blue } You can also change the [shared directory]({% link settings-qemu/sharing.md %}) if using WebDAV. **macOS**{: .label .label-green } You can also download and mount the [Windows guest tools]({% link guest-support/windows.md %}) in this menu. Apple virtualization backend does not support this option.
8. **macOS**{: .label .label-green } The WebDAV [shared directory]({% link settings-qemu/sharing.md %}) can be selected and changed in this menu. Apple virtualization backend does not support this option.
9. Switch between [multiple displays]({% link advanced/multiple-displays.md %}) in this menu.
10. **iOS**{: .label .label-blue } Show or hide the on screen keyboard.
11. **iOS**{: .label .label-blue } Show or hide the other toolbar buttons. When the toolbar is hidden, this button will disappear when no touch event is detected for a long period of time. Tap the screen to reveal the button.
