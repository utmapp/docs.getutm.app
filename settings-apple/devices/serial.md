---
layout: default
title: Serial
parent: Devices
grand_parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Connection

### Mode
* **Built-in Terminal** This serial port will be connected to UTM's built in Terminal which can be configured in the proceeding section.
* **Pseudo-TTY Device** A PTTY device is created and the serial port is redirected to it. Another application can open the device and communicate with the VM. When this option is used, the PTTY device created will be listed in the VM's details on the main window after the VM is started.

## Style
Only applicable in built-in terminal mode.

### Theme
Currently not supported.

### Text Color
Default color of the terminal text.

### Background color
Default color of the terminal background.

### Font
Font of the terminal text.

### Font size
Size of the terminal text.

### Blinking cursor
If enabled, the cursor will pulse on screen.

### Resize Console Command
This is the command that will be sent to the serial device whenever the "Resize" button is pressed in the VM's terminal window. By default it will send `stty cols $COLS rows $ROWS` where `$COLS` and `$ROWS` is determined by the current window size.
