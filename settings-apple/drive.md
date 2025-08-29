---
layout: default
title: Drive
parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Creation

To add a new drive, click "New..." on the sidebar under "Drives".

### Removable
Check "Removable" to create a drive whose image is not stored in the VM's bundle. You can select the image to attach from the home screen.

### Use NVMe Interface
There is some compatibility issues with the (default) VirtIO block storage interface and some Linux distributions. If you are experience disk I/O issues, check this option.

### **macOS 26+**{: .label .label-green } Use Apple Sparse Image Format
Apple Sparse Image Format has better performance and efficiency but is only supported on macOS 26 and higher. If you wish to run this VM on an older macOS host, leave this unchecked.

### Importing

When importing an image, if the drive is not removable, then the image will be copied to the .utm package. Only raw images are supported. If the drive is removable, then no data is copied.

## Deletion

To delete a drive, right/secondary click the drive on the left toolbar and select "Delete".

{: .warning }
When you delete a non-removable drive, the data will be deleted as well. If the drive is removable, no data is deleted.

## Boot Order
The boot order of devices are in the order they appear on the list.

To change the drive order, either right/secondary click the drive on the left toolbar and select "Move Up"/"Move Down" or drag and drop the drive in the desired order.

## Size
When creating a new image, this is the size of the new image. You can toggle between "MB" (mebibyte) or "GB" (gibibyte).

A raw empty image will be created inside the .utm package. If the host file system containing the .utm is APFS, then a sparse file will be created (zeros will not take space).
