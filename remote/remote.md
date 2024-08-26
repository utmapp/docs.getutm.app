---
layout: default
title: Remote
permalink: /remote/
has_children: true
nav_order: 10
---
UTM Remote is a companion to UTM (for macOS) which allows you to connect to your virtual machines running on macOS from another device. It allows you to use UTM as a Virtual Desktop Infrastructure (VDI) and self-host a virtual machine for remote use.

## Getting UTM Remote
The easiest way is for free through the App Store.

[ Download on the App Store](https://apps.apple.com/us/app/utm-remote-virtual-machines/id6470773592){: .btn .btn-blue }

## Setup
UTM Remote requires UTM for macOS to use. [Installation instruction can be found here]({% link installation/macos.md %}) and [server setup guide can be found here]({% link remote/server.md %}).

## Getting Started

{: .screenshots }
[![]({% link assets/images/iphone-remote-start.png %})]({% link assets/images/iphone-remote-start.png %})

1. Discovered and saved servers are listed here. UTM Remote uses Bonjour to automatically discover UTM server running on the same network.
2. Press the "New" button to manually add a server. This is used if you cannot use Bonjour or if the server is located outside of the local network. Note that UTM server must be [configured to accept external clients]({% link preferences/macos.md %}#allow-access-from-external-clients) if this is the case.

{: .screenshots }
[![]({% link assets/images/iphone-remote-add.png %})]({% link assets/images/iphone-remote-add.png %})

1. The name to display in the server list. If left blank, the server list will use the host name instead. If the server was discovered, this will be pre-populated with the host name and can be changed.
2. Type in the host name, IPv4 address, or IPv6 address of the remote server. If the server was discovered, this field will not be modifiable.
3. Type in the port number that the server is listening on. UTM server attempts to use UPnP and NAT-PMP to automatically configure your router when external clients are allowed. However, this may not work and will require manual port forwarding on your router. This field is not available if the server was discovered.
4. The Connect button will be disabled until all required fields are filled in.

## Pairing
Upon first connection, both the server and the client are presented with the fingerprint which **should match unless a third party is eavesdropping**.

{: .screenshots }
[![]({% link assets/images/iphone-remote-trust-alert.png %})]({% link assets/images/iphone-remote-trust-alert.png %})

{: .warning }
Make sure you manually validate that the fingerprint matches what is displayed on the host running UTM server before trusting the connection. A trusted server is able to read and write data on the remote client device.

Once you validated the fingerprint, press "Trust" to continue.

## Password
If the server requires a password, you will be prompted to enter the password. This password can be set in the [server's preferences]({% link preferences/macos.md %}#require-password). You can choose to save the password on the client to avoid having to enter it each time.

{: .warning }
The password is only an additional safeguard that is sent after pairing succeeds. You should always verify the fingerprint before trusting a client or server because an eavesdropper that is trusted can steal the password.

## Usage
Once connected to a server, the interface is [similar to full UTM]({% link basics/basics.md %}).
