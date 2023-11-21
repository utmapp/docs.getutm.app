---
layout: default
title: Linux
parent: Guest Support
---
{% include toc.md %}

## Drivers
Most popular Linux distributions will have the correct drivers already built in. If you are building your own kernel, make sure to include the following options:
* `CONFIG_VIRTIO`
* `CONFIG_VIRTIO_RING`
* `CONFIG_VIRTIO_PCI`
* `CONFIG_VIRTIO_BALLOON`
* `CONFIG_VIRTIO_BLK` for storage devices
* `CONFIG_VIRTIO_CONSOLE` for console devices
* `CONFIG_VIRTIO_NET` for networking
* `CONFIG_DRM_VIRTIO_GPU` for graphical output
* `CONFIG_NET_9P`, `CONFIG_NET_9P_VIRTIO`, `CONFIG_9P_FS`, `CONFIG_9P_FS_POSIX_ACL` for VirtFS directory sharing
* `CONFIG_VIRTIO_FS` for VirtioFS directory sharing

To use the experimental OpenGL hardware acceleration features in the QEMU backend, make sure a [compatible display card is selected]({% link settings-qemu/devices/display.md %}#emulated-display-card) and the VirGL driver is enabled in Mesa.

## SPICE Agent
SPICE agent is required for clipboard sharing (both [QEMU]({% link settings-qemu/sharing.md %}#clipboard-sharing) and [Apple]({% link settings-apple/virtualization.md %}#macos-13-clipboard-sharing) backend) as well as dynamic display resolution in [QEMU]({% link settings-qemu/devices/display.md %}#auto-resolution) backend.

Most distributions will have a package named `spice-vdagent` but you can also build it [from the source](https://gitlab.freedesktop.org/spice/linux/vd_agent). Some common distributions and install instructions are listed below.

### Ubuntu, Debian, apt based

```
$ sudo apt install spice-vdagent
```

### Fedora, CentOS, RPM based

```
$ sudo yum install spice-vdagent
```

{: .note }
These systems will typically already have SPICE agent installed.

### ArchLinux

```
$ sudo pacman -S spice-vdagent
```

## QEMU Agent
Additional features such as time syncing and [scripting]({% link scripting/scripting.md %}) are supported by the QEMU agent.

### Ubuntu, Debian, apt based

```
$ sudo apt install qemu-guest-agent
```

### Fedora, CentOS, RPM based

```
$ sudo yum install qemu-guest-agent
```

### ArchLinux

```
$ sudo pacman -S qemu-guest-agent
```

## SPICE WebDAV
SPICE WebDAV is required for [QEMU directory sharing]({% link settings-qemu/sharing.md %}#spice-webdav) as an alternative to VirtFS.

Once SPICE WebDAV is installed and running, you should be able to access `http://127.0.0.1:9843` from inside the guest. This is a WebDAV share that you can mount using something like `davfs2`.

Most distributions will have a package named `spice-webdavd` or `phodav` but you can also build it [from the source](https://gitlab.gnome.org/GNOME/phodav). Some common distributions and install instructions are listed below.

### Ubuntu, Debian, apt based

```
$ sudo apt install spice-webdavd
```

### Fedora, CentOS, RPM based

```
$ sudo yum install spice-webdavd
```

### ArchLinux

```
$ sudo pacman -S phodav
```

## VirtFS
VirtFS enables [QEMU directory sharing]({% link settings-qemu/sharing.md %}#virtfs) as an alternative to SPICE WebDAV.

After making sure your Linux installation [supports 9pfs](#drivers), you can mount the share with the following command:

```
$ sudo mkdir [mount point]
$ sudo mount -t 9p -o trans=virtio share [mount point] -oversion=9p2000.L
```

Where `[mount point]` is the desired destination path. For example: `/media/share`.

You can also modify `/etc/fstab` and add the following line to automatically mount the share on startup:

```
share	[mount point]	9p	trans=virtio,version=9p2000.L,rw,_netdev,nofail	0	0
```

### Fixing permission errors
You may notice that accessing the mount point fails with "access denied" unless you're the root user. This is because by default the directory inherits the UID/GID from macOS/iOS which has a different numbering scheme. You can fix the error with the following command:

```
$ sudo chown -R $USER [mount point]
```

This will not change the permissions on your host system but will store the guest ownership in a file attribute.

Alternatively, you can install `bindfs` and use the following `/etc/fstab` instead:

```
share	/mnt/macos	9p	trans=virtio,version=9p2000.L,rw,_netdev,nofail	0	0
/mnt/macos    [mount point] fuse.bindfs map=501/1000:@20/@1000,x-systemd.requires=/mnt/macos 0 0
```

## **macOS**{: .label .label-green } VirtioFS
When using Apple Virtualization backend, [directory sharing]({% link settings-apple/sharing.md %}) is enabled through VirtioFS.

{: .note }
VirtioFS is NOT the same as [VirtFS](#virtfs) which is used by the QEMU backend for directory sharing.

After making sure your Linux installation [supports VirtioFS](#drivers), you can mount the share with the following command:

```
$ sudo mkdir [mount point]
$ sudo mount -t virtiofs share [mount point]
```

Where `[mount point]` is the desired destination path. For example: `/media/share`. Note the `share` name above: this is the
exact literal, and all shared folders will appear under it.

Also note: you might need to restart the VM if you've added the first shared directory while the VM was running.

You can also modify `/etc/fstab` and add the following line to automatically mount the share on startup:

```
share	[mount point]	virtiofs	rw,nofail	0	0
```
