---
layout: default
title: Snapshots
parent: Advanced
---
{% include toc.md %}

Snapshots allow you to save the state of a virtual machine at any point and go back to it later. Each snapshot holds the contents of the virtual machine's drives and, when taken from a running QEMU virtual machine, its running state as well.

## Requirements

* **QEMU backend** Supported on macOS and **iOS 26+**{: .label .label-blue } iOS.
* **macOS 27+**{: .label .label-green } **Apple backend** Supported on macOS 27 or higher. The virtual machine must be stopped (or suspended) to create, restore, or overwrite a snapshot.

Snapshots are not available while running in [disposable mode]({% link advanced/disposable.md %}). Only writable disk images that are stored in the virtual machine are included in a snapshot. Removable drives, read-only drives, and external drives are not included.

## Snapshots Tab
Select a virtual machine in the list and choose the "Snapshots" tab below the screenshot in the [details view]({% link basics/basics.md %}). The tab is only shown for virtual machines that support snapshots.

The first entry is the **Current State** of the virtual machine. Below it, every saved snapshot is listed with the newest first. A line along the left edge connects each snapshot to the one it was created from, and a snapshot that was created from a snapshot further down the list shows "From" followed by the name of that snapshot.

### Current State
* **New** Save the current state as a new snapshot. If the QEMU virtual machine is running, the snapshot will include the running state. Otherwise, only the drives are saved (along with the suspended state if the virtual machine is suspended).
* **Overwrite** Replace the snapshot that the current state is based on with the current state. The snapshot keeps its name and its place in the list but what it held before is lost.
* **Delete** Only shown when the virtual machine is suspended. Delete the suspended state so that the virtual machine starts up normally on the next start instead of resuming. Any unsaved data in the suspended state will be lost. Snapshots are not affected.

### Snapshot Actions
Each snapshot has the following actions which are also available from the secondary click (or long press) menu.

* **Restore** Replace the current state of the virtual machine with the snapshot. Any changes that are not saved in another snapshot will be lost. If the snapshot includes the running state, the virtual machine resumes from it the next time it is started. Snapshots marked "Disks Only" do not include the running state so the virtual machine will start up normally. These can only be restored when the virtual machine is not running.
* **Rename** Change the name shown for the snapshot.
* **Delete** Delete the snapshot and all its data.

{: .note }
A snapshot that is marked with "The data of this snapshot is missing." can only be deleted. A snapshot marked with "This snapshot does not cover every drive." is missing from one or more drives (for example, a drive that was added after the snapshot was saved) and cannot be restored.
