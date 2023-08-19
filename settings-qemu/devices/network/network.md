---
layout: default
title: Network
parent: Devices
grand_parent: Settings (QEMU)
has_children: true
---
{% include toc.md %}

## Hardware

### Network Mode
* **Emulated VLAN** Creates a new VLAN and connects this virtual machine to it. This VLAN is created in userspace and requests from the VM will be seen by the host operating system as originating from the UTM process. Different VMs will each have their own VLAN.
* **macOS**{: .label .label-green } **Shared Network** Traffic is routed directly by the host operating system and the guest shares a VLAN with the host. Services running on the guest and the host can see each other without additional configuration. This is recommended for new virtual machines.
* **macOS**{: .label .label-green } **Host Only** Similar to "shared network" except WAN traffic is blocked so the guest cannot access the Internet.
* **macOS**{: .label .label-green } **Bridged** The host creates a layer 2 bridge with the specified interface. This is for advanced users.

### **macOS**{: .label .label-green } Bridged Interface
Only applicable for "bridged" network mode. Note that bridging with an Wifi interface may require additional configuration.

### Emulated Network Card
This is the device seen by the guest operating system. The "virtio-net-pci" card is recommended but may require [additional drivers]({% link guest-support/guest-support.md %}) on the guest to work.

### MAC Address
The MAC address is a unique identifier of the emulated network card.

## Advanced Settings
These settings should not typically be modified and likely does not do what you think they do! They do not allow you to resolve issues where you cannot see a network device.

### Isolate Guest from Host
If enabled, this will block the guest operating system from connecting to the host machine on its VLAN.

### Guest Network
This is the IP subnet where the guest IP is picked from.

### Host Address
This is the IP of the host as seen from inside the guest subnet (when not isolated).

### DHCP Start
This is the first IP from the guest subnet where the built-in DHCP assigns from.

### DHCP End
This is the last IP from the guest subnet where the built-in DHCP assigns from. If specified, the subnet mask from "Guest Network" is ignored.

### DHCP Domain Name
(Emulated VLAN only) Domain name of the built in DHCP server.

### DHCP Server
(Emulated VLAN only) IP of the built in DHCP server on the guest subnet.

### DNS Search Domains
(Emulated VLAN only) DNS search domain.
