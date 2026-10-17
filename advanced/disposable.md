---
layout: default
title: Disposable
parent: Advanced
---
Disposable mode allows you to run a virtual machine without saving any persistent changes to any mounted drives. Anything written to storage will be lost when the virtual machine is shut down.

{: .note }
Disposable mode is supported on QEMU backend and **macOS 27+**{: .label .label-green } Apple backend.

To run in disposable mode, [open the action menu]({% link basics/actions.md %}) and select "Run without saving changes". While running in disposable mode, the window title will show "Disposable Mode".

When running an Apple backend virtual machine in disposable mode, changes to the EFI variables and macOS auxiliary storage are discarded as well. Any saved suspended state is left untouched and the virtual machine boots up fresh.

The virtual machine state cannot be saved to disk when suspended and [snapshots]({% link advanced/snapshots.md %}) cannot be taken while running in disposable mode.
