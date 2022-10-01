---
layout: default
title: macOS
parent: Preferences
grand_parent: Advanced
---
{: .label .label-green }
**macOS**

{% include toc.md %}

To access UTM preferences, either press ⌘+, or from the menu bar, select **UTM → Settings...**.

## Application

### Keep UTM Running...
If enabled, when every window is closed and there are no headless VMs running, UTM will quit as well.

## Display

### VM display size is fixed
If enabled, do not allow resizing of the VM window. If disabled, resizing the VM window will zoom/scale the content if SPICE guest tools are not installed or the VM uses Apple backend. If SPICE guest tools are installed and the VM uses the QEMU backend and this option is disabled, the guest will attempt to change resolution to match the window size.

### Do not save VM screenshot...
For privacy reasons, you may not want UTM to automatically capture a screenshot every 30 seconds and store it in the .utm package. Note that existing screenshots will not be deleted until the next time the VM is started.

## Input

### Hold Control for right click
This is in addition to the usual way of generating a right click which is based on the system preference for a secondary click.

### Use Command+Option for input capture/release
The default combination is Control+Option which can be used to capture/release the mouse when inside a VM window. That button combination collides with the VoiceOver's hot key.

### Caps Lock treated as a key
By default, Caps Lock is treated as a modifier state which is synchronized with the guest. However, some users (for example users of screen reader software) may find it useful to treat Caps Lock as a raw key. If enabled, the Caps Lock state may go out of sync with the host.

### Invert scrolling
Scroll wheel and gestures are translated to mouse wheel events sent to the guest. If this option is enabled, the polarity of the event is inverted.

## USB

### Do not prompt...
When a new USB device is plugged in, the currently active VM will ask the user if they wish to connect the device to the VM. This option will disable that prompt.
