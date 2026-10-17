---
layout: default
title: Remote Control
parent: Advanced
---
{% include toc.md %}

## URL Scheme
The URL scheme `utm` is still associated with the UTM app. Opening the URL `utm://` (for example from Safari or the Shortcuts "Open URLs" action) will launch UTM or bring it to the foreground.

### Download a VM
`utm://downloadVM?url=<url>` downloads a ZIP file containing a `.utm` package, then extracts and imports it. UTM will ask you to confirm before the download starts. The `url` parameter must be URL encoded. For example, `utm://downloadVM?url=https%3A%2F%2Fexample.com%2FVM.zip` downloads `https://example.com/VM.zip`.

### Removed Commands
{: .warning }
The `utm://` URL automation commands (`start`, `stop`, `restart`, `pause`, `resume`, `sendText`, and `click`) were removed in UTM v4.5.1 because they could be abused by a web page to launch a virtual machine without the user's knowledge. Use [Shortcuts or the AppleScript interface]({% link scripting/scripting.md %}) instead.

The removed commands are available as [Shortcuts actions]({% link scripting/scripting.md %}#shortcuts) on **macOS 13+**{: .label .label-green } and **iOS 16+**{: .label .label-blue }. On macOS, they are also available through [AppleScript]({% link scripting/cheat-sheet.md %}) and the [`utmctl`]({% link scripting/scripting.md %}#command-line-interface) command line tool.

| Removed URL command | Shortcuts action | `utmctl` |
|-|-|-|
| `start` | Start Virtual Machine | `utmctl start` |
| `stop` | Stop Virtual Machine | `utmctl stop` |
| `restart` | Restart Virtual Machine | |
| `pause` | Pause Virtual Machine | `utmctl suspend` |
| `resume` | Resume Virtual Machine | `utmctl start` |
| `sendText` | Send Keystrokes | |
| `click` | Send Mouse Click | |

## **macOS**{: .label .label-green } Start a VM automatically when you log in
1. In the Shortcuts app, create a new shortcut with the "Start Virtual Machine" action from UTM and select the virtual machine to start.
2. Select the shortcut in the list and choose File → Add to Dock.
3. Hold down the ⌘ (Command) key while clicking on the new icon in the Dock to reveal the shortcut in Finder (it is in `~/Applications`).
4. Add it to your [Login Items](https://support.apple.com/guide/mac-help/open-items-automatically-when-you-log-in-mh15189/mac) in System Settings → General → Login Items.

To stop the VM from starting at login, remove the shortcut from the Login Items list.

You can also use [headless mode]({% link advanced/headless.md %}) to run the VM without a window.
