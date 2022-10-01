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

### Importing

When importing an image, if the drive is not removable, then the image will be copied to the .utm package. Only raw images are supported. If the drive is removable, then no data is copied.

## Deletion

To delete a drive, right/secondary click the drive on the left toolbar and select "Delete".

{: .warning }
When you delete a non-removable drive, the data will be deleted as well. If the drive is removable, no data is deleted.

## Removable Drive
Non-removable drives are stored in the .utm package. Removable drives only store a bookmark to the drive image and should be used for ISOs and other disk images.

## Size
When creating a new image, this is the size of the new image. You can toggle between "MB" (mebibyte) or "GB" (gibibyte).

A raw empty image will be created inside the .utm package. If the host file system containing the .utm is APFS, then a sparse file will be created (zeros will not take space).
