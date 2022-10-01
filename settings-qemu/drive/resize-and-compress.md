---
layout: default
title: Resize and Compress
parent: Drive
grand_parent: Settings (QEMU)
---
{% include toc.md %}

{: .label .label-green }
**macOS**

On macOS, when you select a non-removable drive, you have additional options to resize and compress the drive image.

{: .warning }
When any of these options are used on a raw image or a non-QCOW2 format image, the image will be converted to QCOW2. All these options are experimental and you should back up your virtual machine before using them.

## Reclaim Space
A re-conversion to QCOW2 is performed and any zeros in the file will be released, freeing up host space. For the best result, first make sure the drive is mounted on a supported interface and the guest operating system supports TRIM. Then, make sure the guest mounts the drive TRIM-aware. On Linux, the `fstrim` can be used to force a TRIM command. After running TRIM, shut down the VM and reclaim space from the drive's settings page to free up the host space.

## Compress
This does the same thing as "reclaim space" (re-coverts to QCOW2) but additionally the data is zstd compressed. Note that when the disk image is used data will not be written back compressed. The compression is done one-time when triggered from the settings page.

## Resize
The QCOW2 image can be resized to be larger. This does not consume host storage right away but allows the guest to grow the size up to the new limit. Once you resized the drive in the settings, make sure the guest operating system also resizes the file system to take advantage of the new space.
