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

Run the tool without any arguments to see the help documentation and a list of available commands.
