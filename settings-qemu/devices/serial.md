---
layout: default
title: Serial
parent: Devices
grand_parent: Settings (QEMU)
---
{% include toc.md %}

## Connection

### Mode
* **Built-in Terminal** This serial port will be connected to UTM's built in Terminal which can be configured in the proceeding section.
* **TCP Client Connection** A TCP connection will be opened and if successful, the serial port will read and write to that socket.
* **TCP Server Connection** A new socket is opened and the serial port will be connected to it. A client can connect to it in order to read and write to the serial port.
* **macOS**{: .label .label-green } **Pseudo-TTY Device** A PTTY device is created and the serial port is redirected to it. Another application can open the device and communicate with the VM. When this option is used, the PTTY device created will be listed in the VM's details on the main window after the VM is started.

### Target
* **Automatic** QEMU provides routing for up to four serial devices automatically. The rules differ for each architecture and system target but they typically map to the main serial ports of the system.
* **Manual** A new serial device can be created in the proceeding section.
* **GDB Debug Stub** A gdbserver stub provided by QEMU can be mapped to the connection.
* **QEMU Monitor** The QEMU monitor (HMP) can be mapped to the connection.

### Wait for Connection
Only applicable in TCP Server mode. When the VM is started, wait until a client is connected before booting up the guest.

### Allow Remote Connection
Only applicable in TCP Server mode. If disabled, the server will listen only on local loopback (127.0.0.1). If enabled, the server will listen on all interfaces (0.0.0.0).

## Hardware
Only applicable if the target is manual.

### Emulated Serial Device
The hardware serial device to emulate for the guest operating system.

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

## TCP
Only applicable in TCP mode.

### Server Address
Only applicable in TCP client mode. This is the server to connect to.

### Port
The TCP port to listen on (server mode) or connect to (client mode).
