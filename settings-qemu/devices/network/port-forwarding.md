---
layout: default
title: Port Forwarding
parent: Network
grand_parent: Devices
---
{% include toc.md %}

Port forwarding is only available on QEMU backend virtual machines using Emulated VLAN network mode. To create a new port forward, press the "New..." button and fill in the fields. To modify an existing port forward, either double click on the entry in the table or select an entry and click "Edit...". On macOS 11, click on an entry to modify it.

## Protocol
Only TCP and UDP are supported.

## Guest Address
Leave this blank (recommended) to indicate all addresses in the guest subnet. Otherwise, this is the IP that should be forwarded.

## Guest Port
Port number to forward from the guest.

## Host Address
Leave this blank (recommended) to indicate the local loopback interface. Otherwise, this is the IP of the interface to listen on.

## Host Port
Port number on the host address to listen on.
