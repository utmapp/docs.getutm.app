---
layout: default
title: UTM Server
parent: Remote
---
To use UTM server on macOS, you must be on version 4.5.2 or higher. Currently, only QEMU backend virtual machines are supported.

## Getting Started
To open UTM server, you can either select the "Server" button from the home screen or the "UTM Server" option from the "Window" menu.

{: .screenshots }
[![]({% link assets/images/macos-server-button.png %})]({% link assets/images/macos-server-button.png %})
[![]({% link assets/images/macos-server-window.png %})]({% link assets/images/macos-server-window.png %})

## Usage

{: .screenshots }
[![]({% link assets/images/macos-server-window.png %})]({% link assets/images/macos-server-window.png %})

1. This enables UTM server when checked. By default, UTM server will not start automatically and this must be checked on every launch of UTM. If you want to automatically start UTM server on launch, [you can change the preferences]({% link preferences/macos.md %}#automatically-start-utm-server).
2. The last known hostname or IP address of the connected client. Note that this may change as the client moves to a different network as well as spoofed by attackers so you should always use the fingerprint to determine a unique client.
3. Each fingerprint is generated from the unique pair of server cryptographic identity and client cryptographic identity.
4. The time of last successful connection.
5. This can be "Connected" indicating that the client is currently connected or "Blocked" indicating that the client was rejected by the user. If this is a unknown client, options to Approve or Block the client will be presented here if the connection notification was ignored.
6. The current status of the server which can be "Running" or "Stopped"
7. This will reset the server identity, disconnect all clients, and invalidate all trusted clients. This can be used for troubleshooting server issues but be aware that since the server identity changed, all fingerprints saved on paired clients will be invalid and will show an error on the next connection attempt. The client must remove the paired server and re-establish trust.

## Settings
UTM server settings can be found in [Preferences]({% link preferences/macos.md %}#server).

## Pairing
Upon first connection, both the server and the client are presented with the fingerprint which **should match unless a third party is eavesdropping**. A notification will pop-up containing the fingerprint. You should verify with the fingerprint which is displayed on the device and press "Options → Accept" only if the fingerprint matches. If you missed the notification, you can find the client listed in the server window and you can select Approve/Block from the status column.

{: .screenshots }
[![]({% link assets/images/macos-server-prompt.png %})]({% link assets/images/macos-server-prompt.png %})

{: .warning }
Make sure you manually validate that the fingerprint matches on the device before accepting the connection. If the fingerprint does not match or you did not initiate a connection yourself, you should deny the connection. A trusted client is able to read and write data on the host machine.

## Removing Clients
To remove a client, in the server window, select the client with the fingerprint you wish to remove and perform a secondary (right) click. This should open up a menu allowing you to "Block" or "Delete" the client.
