---
layout: default
title: Directory
parent: Sharing
grand_parent: Guest Support
---
{% include toc.md %}

Directory sharing allows a host directory to be shared with the guest. There are three supported backends for directory sharing:

1. **SPICE WebDAV** Requires SPICE webdavd to be installed and creates a local WebDAV server that is connected to the host. It is supported only by the QEMU backend and is compatible with Windows and Linux guests.
2. **VirtFS** Requires 9pfs drivers and is currently only supported by the QEMU backend running Linux. It has better transfer speeds than SPICE WebDAV.
3. **macOS 12+**{: .label .label-green } **VirtioFS** Requires virtiofs drivers and is currently only supported by the Apple backend running Linux.

{: .note }
**macOS**{: .label .label-green } Shared directories in macOS VMs are only available in macOS 13 and later (both guest and host).

## Selecting directory to share
This can be done [from the details view]({% link basics/basics.md %}) near the bottom of the view.

## Mounting on guest
Windows guests can install [the guest tools]({% link guest-support/windows.md %}) to enable SPICE WebDAV sharing. Linux guests have [a variety of options]({% link guest-support/linux.md %}) for directory sharing.
