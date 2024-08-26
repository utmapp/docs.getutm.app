---
layout: default
title: macOS
parent: Preferences
---
{: .label .label-green }
**macOS**

{% include toc.md %}

To access UTM preferences, either press ⌘+, or from the menu bar, select **UTM → Settings...**.

## Application

### Keep UTM Running...
If enabled, when every window is closed and there are no headless VMs running, UTM will quit as well.

## **macOS 13+**{: .label .label-green } Show dock icon
If disabled, on next launch, the dock icon will be hidden. This is useful for [headless mode]({% link advanced/headless.md %}). If this option is disabled, the menu bar icon must be shown and UTM will keep running even if all windows are closed.

## **macOS 13+**{: .label .label-green } Show menu bar icon
If enabled, a menu bar extra for UTM will be displayed. This allows you to quickly start and stop a VM as well as quit UTM.

## Prevent system from sleeping...
If enabled, system idle sleep will be disabled when *any* VM is running (including headless ones).

## Do not show confirmation when closing...
UTM will warn you when you attempt to close a window of a running VM or when you attempt to quit the application while there are still running VMs. Not properly shutting down a guest could result in data loss. This option will disable the prompt.

## Display

### Do not save VM screenshot...
For privacy reasons, you may not want UTM to automatically capture a screenshot every 30 seconds and store it in the .utm package. Note that existing screenshots will not be deleted until the next time the VM is started.

### Renderer Backend
When a QEMU backend VM supports [GPU acceleration]({% link settings-qemu/devices/display.md %}#emulated-display-card), one of a number of renderer backends can be selected. There are certain applications that only work (or performs better) with a specific backend. If you are unsure, leave it to default.

### FPS Limit
By default, the operating system will synchronize the rendering of each frame to the refresh rate of the current display. However, there are cases where performance intensive applications may cause frame stalls and result in inconsistent frame times. You can use this option to lower the target frame rate in order to have a more consistent experience.

## Sound

### Sound Backend
This allows you to specify the audio backend for QEMU VMs. The default will select the best available backend. If the selected backend is not available for any reason, it will fallback to another option. CoreAudio has lower latency but does not support audio input (microphone).

## Input

### Capture input automatically when entering full screen
Only for QEMU backend VMs. When full screen is entered, the cursor and keyboard input will automatically be captured. In order to release the capture, you must use the capture/release hotkey (Control+Option unless changed).

### Capture input automatically when window is focused
Only for QEMU backend VMs. When a VM is started or when a VM window is clicked on, the cursor and keyboard input will be captured.

### Option is Meta key
When using the built-in console, the Option key can be used as the Meta key. This means that the Esc key is set before the character that was pressed. This is useful for applications like Emacs which makes use of the Meta key. The downside is that international text entry is also handled by the Option key and so enabling this breaks that. You can toggle this option (per-window) while using the console with the key shortcut Command+Option+O.

### Hold Control for right click
This is in addition to the usual way of generating a right click which is based on the system preference for a secondary click.

### Use Command+Option for input capture/release
The default combination is Control+Option which can be used to capture/release the mouse when inside a VM window. That button combination collides with the VoiceOver's hot key.

### Caps Lock treated as a key
By default, Caps Lock is treated as a modifier state which is synchronized with the guest. However, some users (for example users of screen reader software) may find it useful to treat Caps Lock as a raw key. If enabled, the Caps Lock state may go out of sync with the host.

### Num Lock is forced on
For keyboards which do not have a num lock button, this will ensure the guest always treat the numeric pad as number keys. Since macOS does not support num lock, we do not attempt to synchronize the host num lock state (and keyboard LED) so this may result in the guest and host having the num lock state out of sync.

### Invert scrolling
Scroll wheel and gestures are translated to mouse wheel events sent to the guest. If this option is enabled, the polarity of the event is inverted.

## USB

### Do not prompt...
When a new USB device is plugged in, the currently active VM will ask the user if they wish to connect the device to the VM. This option will disable that prompt.

## Server

## Automatically start UTM server
When checked, UTM server will attempt to start immediately if it is not already started. UTM server will also start when UTM is launched.

## Reject unknown connections by default
New clients must be trusted by the host before they can connect. When a new client attempts to connect, you will receive a notification allowing you to check the fingerprint and then accept or reject the connection. If a connection is rejected, the notification will not show up for any connection attempts and must be manually accepted in the client list. When this option is checked, every connection attempt will be rejected by default (showing no notification) and each connection must be manually reviewed and trusted in the client list.

## Allow access from external clients
By default, UTM server will only permit connections from the local network (LAN). When this option is checked, UTM server will permit connections from outside the local network (WAN) including the internet if your router is set up correctly to forward traffic.

## Listen port
By default, UTM server communicates with UPnP which allocates a UDP port dynamically and is discoverable through Bonjour to other devices on the same network. If you put in a port number, UTM server will also listen on that TCP port for connections. This is required if you allow access from external clients.

## Require password
When checked, clients must provide the correct password (as specified in the text field below) in order to attempt a connection. This option is highly recommended if you choose to allow access from external clients.
