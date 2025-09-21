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
VirtFS enables [QEMU directory sharing]({% link settings-qemu/sharing.md %}#virtfs) as an alternative to SPICE WebDAV. Note that VirtFS sharing must be enabled in the settings and you cannot use it at the same time as WebDAV directory sharing.

After making sure your Linux installation [supports 9pfs](#drivers), you can automatically mount the share by adding the following entry to your `/etc/fstab`:

```
# UTM Shared Folder
share /mnt/utm 9p trans=virtio,version=9p2000.L,rw,_netdev,nofail,auto 0 0
```

_Note_: `share` is the name UTM uses for the VirtIO device and you should not change it. You can replace `/mnt/utm` with a different folder if you like.

After updating `/etc/fstab` you need to create an empty folder for the mount:

```sh
sudo mkdir /mnt/utm
```

You can apply the changes to `/etc/fstab` with the following commands (this will automatically happen on reboot as well):

```sh
systemctl daemon-reload
systemctl restart network-fs.target # use remote-fs.target if not found
systemctl list-units --type=mount
```

A systemd `.mount` unit for `/mnt/utm` should now be displayed in the list, and you can access the contents of your shared folder.

### Fixing permission errors
You may notice that accessing the mount point fails with "access denied" unless you're the root user. This is because by default the directory inherits the UID/GID from macOS/iOS which has a different numbering scheme.

To fix this we are going to use [`bindfs`](https://bindfs.org/) to create a mount in the user's home directory that we can access normally. You have to first install `bindfs` with your system's package manager.

The first step is to get the UID and GID used by the host:

```
$ ls -na /mnt/utm
total 8
drwxr-xr-x 4 502 20  128 Feb 22 15:52 .
drwxr-xr-x 3   0  0 4096 Feb 22 14:50 ..
-rw-r--r-- 1 502 20   13 Feb 22 15:52 shared-file.txt
```

In this case the UID for the host is `502` and the GID is `20`. You have to do the same for the guest user (usually UID `1000` and GID `1000`). Additionally, create an empty folder for the `bindfs` mount in the home directory:

```sh
mkdir /home/user/utm
```

_Note_: In this example the username is `user`, you might have to adjust this to match your configuration.

Now add another entry to `/etc/fstab`:

```
# bindfs mount to remap UID/GID
/mnt/utm /home/user/utm fuse.bindfs map=502/1000:@20/@1000,x-systemd.requires=/mnt/utm,_netdev,nofail,auto 0 0
```

An alternative solution is to recursively change the permissions of the files in your shared folder:

```
$ sudo chown -R $USER /mnt/utm
```

_Note_: This will not change the permissions on your host system, but it will add a custom `user.virtfs` file attributes to every file to store the guest ownership. It is not recommended to do this if you want to share your host's home folder for instance.

## **macOS**{: .label .label-green } VirtioFS
When using Apple Virtualization backend, [directory sharing]({% link settings-apple/sharing.md %}) is enabled through VirtioFS.

{: .note }
VirtioFS is NOT the same as [VirtFS](#virtfs) which is used by the QEMU backend for directory sharing. The name for mounting the shared directory is always `share` — it’s not the same as the folder name you chose when configuring the VM in UTM.

After making sure your Linux installation [supports VirtioFS](#drivers), you can mount the share with the following command:

```
$ sudo mkdir [mount point]
$ sudo mount -t virtiofs share [mount point]
```

Where `[mount point]` is the desired destination path. For example: `/media/myshare`.

You can also modify `/etc/fstab` and add the following line to automatically mount the share on startup:

```
share	[mount point]	virtiofs	rw,nofail	0	0
```
