---
layout: default
title: Network
parent: Devices
grand_parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Hardware

### Network Mode
* **Shared Network** Traffic is routed directly by the host operating system and the guest shares a VLAN with the host. Services running on the guest and the host can see each other without additional configuration. This is recommended for new virtual machines.
* **macOS 26+**{: .label .label-green } **NAT Network** Virtual machines using this mode in the same UTM app can connect to each other and access the internet through your Mac.
* **macOS 26+**{: .label .label-green } **Host Only** Virtual machines using this mode in the same UTM app can connect to each other and your Mac. This network does not provide internet access.
* **Bridged (Advanced)** The host creates a layer 2 bridge with the specified interface. This is for advanced users.

### Bridged Interface
Only applicable for "bridged" network mode. Note that bridging with an Wifi interface may require additional configuration.

### MAC Address
The MAC address is a unique identifier of the emulated network card.
