---
layout: default
title: iOS
parent: Preferences
---
{: .label .label-blue }
**iOS**

{% include toc.md %}

The preferences can be accessed from the iOS Settings application under "UTM".

**WIP**{: .label .label-yellow } If UTM is installed using TrollStore, the preferences will be inaccessible. You can manually edit the preferences data using a 3rd party application.

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

### FPS Limit
By default, the operating system will synchronize the rendering of each frame to the refresh rate of the current display. However, there are cases where performance intensive applications may cause frame stalls and result in inconsistent frame times. You can use this option to lower the target frame rate in order to have a more consistent experience.

## Gestures
Various actions can be mapped to gestures.

* **Click & Hold** Performs a left mouse click that will be released when the finger leaves the screen.
* **Right Click** Performs a right click and release.
* **Move Screen** Move the VM display around. Note if any gesture is set to this action, then the pinch gesture will also be enabled to scale the display.
* **Mouse Wheel** Sends a mouse wheel event corresponding to the gesture direction.

## Cursor

* **Drag cursor** A movement is translated to a relative movement of the cursor on screen. Mouse acceleration is enabled when this option is used.
* **Touch mode (always show cursor)** The absolute position of the input event is passed to the VM. Note that the guest must support the emulated USB tablet device for this option to work.
* **Touch mode (try hiding cursor)** Same as above but when supported with the right emulated display card, the cursor will not be drawn on screen.

### Drag Speed
This can be used to adjust the mouse acceleration.

### Invert Scroll
Scroll wheel and gestures are translated to mouse wheel events sent to the guest. If this option is enabled, the polarity of the event is inverted.

## Gamepad
When a supported gamepad is attached, the buttons can be mapped to keyboard keys.

### Cursor Speed
The analog stick on the gamepad can function as a mouse. This option controls the acceleration.

## Jitstreamer
[Jitstreamer](https://github.com/jkcoxson/JitStreamer) can be set up here.
