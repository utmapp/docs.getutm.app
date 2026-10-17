---
layout: default
title: Scripting
nav_order: 9
has_children: true
---
{: .label .label-green }
**macOS**

{% include toc.md %}

UTM provides power users with access to Shortcuts intents and an AppleScript bridge interface paired with a command line interface. Note that not all features are currently supported in the automation interface and feedback is welcome on what should be added.

## Shortcuts
UTM provides basic actions to the Shortcuts app which you can use to build a workflow. Currently, there exists actions to:
* Find a virtual machine by keywords and/or its status
* Start/stop/pause/resume/restart a virtual machine
* Send keystrokes and mouse clicks to a running virtual machine

## AppleScript
For more advanced automation, UTM provides an AppleScript interface. Details on the verbs and nouns available in the scripting interface can be found [here]({% link scripting/reference.html %}) or in the AppleScript dictionary. To browse the dictionary:

1. Open "Script Editor" (found in Applications → Utilities)
2. In the menu bar choose File → Open Dictionary... (or Shift+Cmd+O)
3. Select UTM from the list of applications

Check out the [cheat sheet]({% link scripting/cheat-sheet.md %}) for some examples of what you can do.

## Command Line Interface
The CLI tool is a wrapper around the AppleScript interface and provides easy access to some of the functionality. It can be found at:

```
/Applications/UTM.app/Contents/MacOS/utmctl
```

It is recommended you "install" this by creating a symbolic link to your `bin` directory:

```
$ sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin/utmctl
```

If you installed UTM to another directory, the symbolic link will not work properly. Instead, you need to add the directory containing `utmctl` to your PATH variable:

```
$ echo "/path/to/UTM.app/Contents/MacOS" | sudo tee /etc/paths.d/10-utm
```

Run the tool without any arguments to see the help documentation and a list of available commands. Run `utmctl help <command>` to see the options for a specific command. Virtual machines are identified by either their UUID or their complete name.

| Command | Description |
|-|-|
| `version` | Display the version number of UTM. |
| `list` | List all registered virtual machines. |
| `status` | Query the status of a virtual machine. |
| `start` | Start a virtual machine or resume a suspended virtual machine. Use `--disposable` to run without saving changes and `--recovery` to boot a macOS guest in recovery mode. |
| `suspend` | Suspend a running virtual machine to memory. |
| `stop` | Shut down a running virtual machine. |
| `attach` | Redirect the serial input/output to this terminal. |
| `file pull`, `file push` | Copy a file from or to the guest (requires the guest agent). |
| `exec` | Execute an application on the guest (requires the guest agent). |
| `ip-address` | List the IP addresses of the guest. |
| `clone` | Clone an existing virtual machine. |
| `delete` | Delete a virtual machine (there is no confirmation). |
| `discard-state` | Discard the saved state of a suspended virtual machine so that it starts up normally. |
| `usb list`, `usb connect`, `usb disconnect` | List USB devices and connect or disconnect them from a virtual machine. Devices are identified by a `VID:PID` pair or by the location shown in `usb list`. |
| `snapshot list`, `create`, `restore`, `overwrite`, `rename`, `delete`, `scan` | Manage the [snapshots]({% link advanced/snapshots.md %}) of a virtual machine. Snapshots are identified with `--snapshot` by either their name or their identifier. |

### Examples

```
$ utmctl snapshot create "Ubuntu" --name "Before update"
$ utmctl snapshot list "Ubuntu" --json
$ utmctl snapshot restore "Ubuntu" --snapshot "Before update"
$ utmctl usb connect "Ubuntu" 05AC:12A8
```

### **macOS 27+**{: .label .label-green } Setting up a macOS guest
When starting a newly installed macOS guest for the first time, `utmctl start` can create the user account without any interaction. This requires macOS 27 or later on both the host and the guest and only works on the first start after macOS is installed.

```
$ utmctl start "macOS" --provision-username user --provision-password-stdin --provision-auto-login --provision-ssh
```

The options are:
* `--provision-username` The short name of the account to create.
* `--provision-full-name` The full name of the account (defaults to the username).
* `--provision-password` or `--provision-password-stdin` The password of the account. Other processes can see a password passed on the command line so reading it from standard input is recommended.
* `--provision-auto-login` Log in to the account automatically when the guest starts up.
* `--provision-ssh` Turn on Remote Login (SSH) in the guest.
