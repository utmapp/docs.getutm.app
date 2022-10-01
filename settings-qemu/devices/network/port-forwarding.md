---
layout: default
title: Port Forwarding
parent: Network
grand_parent: Devices
---
{% include toc.md %}

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
