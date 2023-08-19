---
layout: default
title: macOS
parent: Guest Support
---
{% include toc.md %}

{: .label .label-green }
**macOS 12+**

macOS guests are supported on Apple Silicon hosts running macOS 12 or higher.

## Installation
In the [new VM wizard]({% link basics/basics.md %}), select "Virtualization" and then "macOS 12+" to install macOS as a guest. If either option is not available, your system does not support macOS guests.

### IPSW
Apple distributes macOS software in an IPSW file. UTM can download the latest compatible macOS automatically if you do not select an IPSW. You can also download IPSWs from a third party site such as [ipsw.me](https://ipsw.me/VirtualMac2,1).

{: .warning }
We do not attest to the safety, validity, or compatibility of IPSws downloaded from third party sites such as ipsw.me. We recommend using UTM's automatic download of the most compatible IPSW.

## Shared Directories

### VirtioFS
{: .label .label-green }
**macOS 13+**
When both the guest and host are running macOS 13 or higher, shared directories can be mounted as a network volume. You can mount the volume from Terminal:

```
$ mkdir -m 777 -p [mount point]
$ mount_virtiofs share [mount point]
```

`[mount point]` can be any valid path such as `/Volumes/Share` as an example.

### Network sharing
Another way of sharing files between the host and guest (including support for macOS 12) is to use the network file sharing feature of macOS running on the host. You can do it from "System Preferences" under the "Sharing" category. Check out [Apple's user guide](https://support.apple.com/guide/mac-help/set-up-file-sharing-on-mac-mh17131/mac) for more details. Once a network share is set up, your macOS guest can connect to it just like any other Mac.

## Missing features
The Apple Virtualization backend used to virtualize macOS does not support many UTM features. Below is a list of some unsupported features.

* USB sharing
* Clipboard sharing
* Dynamic display resolution
* Save states
