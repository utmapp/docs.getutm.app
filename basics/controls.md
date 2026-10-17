---
layout: default
title: Controls
parent: Basics
nav_order: 2
---

{: .screenshots }
[![]({% link assets/images/macos-vm-toolbar.png %})]({% link assets/images/macos-vm-toolbar.png %})
[![]({% link assets/images/iphone-vm-toolbar.png %})]({% link assets/images/iphone-vm-toolbar.png %})

1. Power off the virtual machine. This will discard any unsaved data. It is recommended that you shut down the virtual machine from the guest operating system. **macOS**{: .label .label-green } You can click and hold this button for additional power-down options:
    1. *Request power down*: Sends power down request to the guest. This simulates pressing the power button on a PC.
    2. *Force shut down*: Tells the VM process to shut down with risk of data corruption. This simulates holding down the power button on a PC. This is the default option.
    3. *Force kill*: Force kill the VM process with high risk of data corruption.
2. Suspend the virtual machine when supported.

{: .note }
The suspend feature will not work if any device that is in use does not support suspend. This typically includes emulated NVMe devices as well as GPU accelerated display cards. Additionally, QEMU hypervisor on Intel does not support suspend.

{: style="counter-reset:none" }
3. Reset the virtual machine. This will discard any unsaved data.
4. **macOS**{: .label .label-green } Capture the cursor and keyboard for exclusive use by the virtual machine. This allows certain key combinations such as Cmd+Tab to be sent to the virtual machine. Once captured, the [key combination Control+Option]({% link preferences/macos.md %}#use-commandoption-for-input-capturerelease) can be used to release the capture. The same key combination can also be used to enter capture mode as well.
5. **iOS**{: .label .label-blue } When in graphical display mode, the first press will lock the display to fit. That means whenever the resolution changes, the display will scale accordingly so the entire screen is used. A second press will release the lock and set the display scaling to 1x. When in terminal display mode, a press will send the [resize command]({% link settings-qemu/devices/serial.md %}#resize-console-command). **macOS**{: .label .label-green } This button is only enabled in terminal display mode and has the same behaviour as iOS.
6. USB devices that are currently detected are listed and can be connected or disconnected. See [USB sharing]({% link guest-support/sharing/usb.md %}) for more details. **iOS**{: .label .label-blue } Not all builds support this option. **macOS**{: .label .label-green } Apple virtualization backend requires macOS 27 or higher and only lists devices that are assigned to UTM. If unsupported or if [USB sharing is disabled]({% link settings-qemu/input.md %}#usb-sharing), this button will be disabled or missing.
7. When one or more [removable drives]({% link settings-qemu/drive/drive.md %}) are configured, you can change the mounted image in this menu. **iOS**{: .label .label-blue } You can also change the [shared directory]({% link settings-qemu/sharing.md %}) if using WebDAV. **macOS**{: .label .label-green } You can also download and mount the [Windows guest tools]({% link guest-support/windows.md %}) in this menu. Apple virtualization backend requires macOS 15 or higher for this option.
8. **macOS**{: .label .label-green } The WebDAV [shared directory]({% link settings-qemu/sharing.md %}) can be selected and changed in this menu. For Apple virtualization backend, the [shared directories]({% link settings-apple/sharing.md %}) can be added, changed, removed, and set to read only in this menu.
9. Switch between [multiple displays]({% link advanced/multiple-displays.md %}) in this menu.
10. **iOS**{: .label .label-blue } Show or hide the on screen keyboard. You can also Force Touch this button to send a keyboard shortcut. See [below](#ios-keyboard-accessory-bar) for the keys shown above the keyboard.
11. **iOS**{: .label .label-blue } Show or hide the other toolbar buttons. When the toolbar is hidden, this button will disappear when no touch event is detected for a long period of time. Tap the screen to reveal the button.

## **iOS**{: .label .label-blue } Touch Input
Touches on the virtual machine display are translated to mouse input. The action performed by each gesture (such as long press, two finger tap, and two or three finger pan) as well as the cursor mode can be changed in the [preferences]({% link preferences/ios.md %}). In addition to left and right clicks, gestures can be mapped to a middle click as well as to holding the right or middle button for dragging.

* **Touch mode (drag to scroll)** behaves like a touch screen. A tap is a left click, dragging one finger scrolls the content, and a long press that moves turns into a left button drag so windows and selections can still be moved with one finger.
* Touches that start at the top or bottom edge of the screen are sent to the virtual machine first. Swipe a second time to use the system gesture (such as opening Notification Center).
* Pinching to zoom will stop the display from automatically scaling to fit until it is reset with the resize button in the toolbar.

## **iOS**{: .label .label-blue } Keyboard Accessory Bar
When the on screen keyboard is shown, a bar above it provides keys that are missing from the iOS keyboard:

* Modifier keys Control, Option, Command, and Shift which stay pressed until the next key is pressed
* Tab, Escape, arrow keys, and Forward Delete
* F1 through F12
* Caps Lock, Scroll Lock, Num Lock, Print Screen, Insert, Home, End, Page Up, and Page Down
* Paste the iOS clipboard as keystrokes and hide the keyboard

## **iOS 27.1+**{: .label .label-blue } iPhone Duo
On iPhone Duo, the toolbar is placed in the strip beside the camera on the outer display. When the device is folded like a laptop, the virtual machine display is shown on the top half and the bottom half becomes an input deck. The deck can show either the on screen keyboard (with the accessory bar) or a touchpad, and you can switch between them with the keyboard and touchpad buttons in the deck. The choice is remembered the next time the device is folded.

On the touchpad, one finger moves the pointer, a tap clicks, a two finger tap is a right click, two fingers scroll, and holding a finger down for a moment starts a drag. The touchpad is only available for graphical displays. Terminal windows always show the keyboard in the deck.
