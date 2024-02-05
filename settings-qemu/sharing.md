---
layout: default
title: Sharing
parent: Settings (QEMU)
---
{% include toc.md %}

## Clipboard sharing
When this option is enabled and the [SPICE guest tools]({% link guest-support/guest-support.md %}) are installed, the clipboard will be synced between the guest and the host.

## Shared directory
Two methods of directory sharing are supported by UTM.

### SPICE WebDAV
This requires the [SPICE guest tools]({% link guest-support/guest-support.md %}) to be installed on the guest. The shared directory is exposed as a WebDAV mount on the guest's localhost (typically on port 9843). On Linux, you should prefer VirtFS, which is faster. For Windows guests, this is the only option.

For some versions of Windows (tested on Windows 11 23H2), the WebDAV client has a default file size limit of 50 MB.
To increase this in the Registry:

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters]
    "FileSizeLimitInBytes"=dword:ffffffff

### VirtFS
This requires the guest operating system to have driver support for 9pfs and VirtIO. The shared directory is exposed under the VirtFS tag `share`. Note that unlike WebDAV, the shared directory cannot be changed while the VM is powered on. There is currently a lack of Windows support but the performance on Linux is much better so this is the recommended option if you are running Linux. See [this page]({% link guest-support/linux.md %}) for more information.
