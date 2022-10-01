---
layout: default
title: Drive
parent: Settings (QEMU)
has_children: true
---
{% include toc.md %}

## Creation

{: .label .label-green }
**macOS**

To add a new drive, click "New..." on the sidebar under "Drives".

{: .label .label-blue }
**iOS**

To add a new drive, tap the "+" button on the top left in the main settings menu and select "Import Drive" or "New Drive".

### Importing

**iOS**{: .label .label-blue } When importing a drive, a removable drive will be created and the selected image will be associated with the new drive.

**macOS**{: .label .label-green } When importing a drive that is non-removable and not a raw image, the selected image will first be converted to the QCOW2 format.

## Deletion

{: .label .label-green }
**macOS**

To delete a drive, right/secondary click the drive on the left toolbar and select "Delete".

{: .label .label-blue }
**iOS**

To delete a drive, swipe left on the drive and tap "Delete".

{: .warning }
When you delete a non-removable drive, the data will be deleted as well. If the drive is removable, no data is deleted.

## Removable Drive
Non-removable drives are stored in the .utm package. Removable drives only store a bookmark to the drive image and should be used for ISOs and other disk images.

## Interface
This is the hardware interface to connect this drive to. Typical users do not need to change from the default interface.

## Image Type
* **None** This drive is not used at all.
* **Disk Image** The drive will be mounted in the bus specified in "interface" with a non-removable media type.
* **CD/DVD (ISO) Image** The drive will be mounted in the bus specified in "interface" with a removable media type.
* **Deprecated**{: .label .label-red } **BIOS** "Interface" is ignored and no drive is emulated. The image will be passed to QEMU through the `-bios` argument.
* **Deprecated**{: .label .label-red } **Linux Kernel** "Interface" is ignored and no drive is emulated. The image will be passed to QEMU through the `-kernel` argument.
* **Deprecated**{: .label .label-red } **Linux RAM Disk** "Interface" is ignored and no drive is emulated. The image will be passed to QEMU through the `-initrd` argument.
* **Deprecated**{: .label .label-red } **Linux Device Tree Binary** "Interface" is ignored and no drive is emulated. The image will be passed to QEMU through the `-dtb` argument.

## Size
When creating a new image, this is the size of the new image. You can toggle between "MB" (mebibyte) or "GB" (gibibyte).

### Raw Image
If selected, a raw empty image will be created inside the .utm package. If the host file system containing the .utm is APFS, then a sparse file will be created (zeros will not take space).

If not selected, a QCOW2 disk image will be created inside the .utm package. The QCOW2 format will grow as the disk image grows.
