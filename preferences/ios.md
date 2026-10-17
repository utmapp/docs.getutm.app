---
layout: default
title: iOS
parent: Preferences
---
{: .label .label-blue }
**iOS**

{% include toc.md %}

The preferences can be accessed from the gear (Settings) button in the toolbar of UTM's home screen. They can also be found in the iOS Settings application under "UTM".

{: .note }
If UTM is installed using TrollStore, UTM will not appear in the iOS Settings application. Use the in-app Settings button instead.

## Background

### Continue running...
If enabled, UTM will request location access in order to keep running in the background. If the VM uses too much memory, the operating system can still decide to terminate it.

{: .notice }
The location data is not stored anywhere and is only used to ensure the operating system does not terminate the application.

### Auto save on background
If enabled, when UTM enters the background, it will attempt to save the current VM state. This means that if the VM is terminated by the operating system, it can be restored in the next launch.

### Auto save on low memory
If enabled, when UTM is running low on memory, it will attempt to save the current VM state. This means that if the VM is terminated by the operating system, it can be restored in the next launch.

## Idle

### Disable screen dimming when idle
This bypasses the system screen dimming settings and forces the display to be always on while the VM is running.

### Do not save VM screenshot to disk
For privacy reasons, you may not want UTM to automatically capture a screenshot every 30 seconds and store it in the .utm package. Note that existing screenshots will not be deleted until the next time the VM is started.

## Devices

### Do not show prompt when USB...
When a new USB device is plugged in, the currently active VM will ask the user if they wish to connect the device to the VM. This option will disable that prompt. This option only applies to builds that support USB.

### Prefer device to external microphone
By default, when a headset is connected (Lightning or Bluetooth), the headset microphone will be used as the microphone device in the VM. However, some users may prefer the higher fidelity microphone that is built into the iOS device and this option will allow that to be used instead.

## Graphics

### Renderer Backend
When a QEMU backend VM supports [GPU acceleration]({% link settings-qemu/devices/display.md %}#emulated-display-card), one of a number of renderer backends can be selected. There are certain applications that only work (or performs better) with a specific backend. If you are unsure, leave it to default.

{: .note }
Only Default and ANGLE (Metal) support Vulkan and DirectX.

### Vulkan Driver
Selects the host Vulkan driver used for [Vulkan passthrough]({% link guest-support/linux.md %}) to a guest with VirtIO Venus drivers.

* **Default**: Currently the same as MoltenVK.
* **Disabled**: Vulkan is not available to the guest.
* **MoltenVK**: Recommended driver.
* **KosmicKrisp** **iOS 26+**{: .label .label-blue }: An experimental Mesa based Vulkan driver.

### DirectX Driver
Selects the host DirectX driver used for [DirectX passthrough]({% link guest-support/windows.md %}) to a Windows guest with the 3D graphics driver installed or Linux guest with Neptune driver installed. On iOS, only DXMT (DirectX 11) is available.

### FPS Limit
When set to "None" (the default), iPad will render at the maximum refresh rate of the display (for example, 120Hz on ProMotion displays) and iPhone will render at 60Hz in order to save battery. You can set this to 120 to use ProMotion on a supported iPhone. There are also cases where performance intensive applications may cause frame stalls and result in inconsistent frame times. You can use this option to lower the target frame rate in order to have a more consistent experience.

## Gestures
Various actions can be mapped to the following gestures: Long Press, Two Finger Tap, Two Finger Pan, Two Finger Swipe, and Three Finger Pan. Not every action is available for every gesture.

* **Click & Hold** Performs a left mouse click that will be released when the finger leaves the screen.
* **Right Click** Performs a right click and release.
* **Middle Click** Performs a middle click and release. This is useful for guests that use the middle button to paste or pan.
* **Right Click & Hold** / **Middle Click & Hold** Holds down the right or middle button while dragging and releases it when the fingers leave the screen.
* **Move Screen** Move the VM display around. Note if any gesture is set to this action, then the pinch gesture will also be enabled to scale the display.
* **Mouse Wheel** Sends a mouse wheel event corresponding to the gesture direction.

## Cursor

### Touch Input
* **Drag cursor** A movement is translated to a relative movement of the cursor on screen. Mouse acceleration is enabled when this option is used.
* **Touch mode (always show cursor)** The absolute position of the input event is passed to the VM. Note that the guest must support the emulated USB tablet device for this option to work.
* **Touch mode (try hiding cursor)** Same as above but when supported with the right emulated display card, the cursor will not be drawn on screen.
* **Touch mode (drag to scroll)** Behaves like a touch screen and does not press any button when a finger lands. A tap is a left click, a long press runs the Long Press action, and dragging one finger scrolls the mouse wheel so the content follows your finger. A long press that then moves turns into a left button drag so windows and selections can still be moved with one finger. A ring is shown when the long press is recognized.

### Apple Pencil Input
* **Drag cursor** Same as the touch option above.
* **Tablet mode (always show cursor)** The absolute position of the pencil is passed to the VM.
* **Tablet mode (try hiding cursor)** Same as above but the cursor will not be drawn on screen when supported.

### Drag Speed
This can be used to adjust the mouse acceleration.

### Invert Scroll
Scroll wheel and gestures are translated to mouse wheel events sent to the guest. If this option is enabled, the polarity of the event is inverted.

## Gamepad
When a supported gamepad is attached, the buttons can be mapped to keyboard keys or mouse buttons.

### Cursor Speed
The analog stick on the gamepad can function as a mouse. This option controls the acceleration.

## JitStreamer
[JitStreamer](https://github.com/jkcoxson/JitStreamer) can be set up here.
