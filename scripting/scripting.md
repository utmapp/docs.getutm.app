---
layout: default
title: Scripting
nav_order: 9
has_children: true
---
{: .label .label-green }
**macOS**

{% include toc.md %}

UTM provides power users with access to an AppleScript bridge interface paired with a command line interface. Note that not all features are currently supported in the scripting interface and feedback is welcome on what should be added.

## AppleScript
Details on the verbs and nouns available in the scripting interface can be found [here]({% link scripting/reference.html %}) or in the AppleScript dictionary. To browse the dictionary:

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
$ sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin
```

Run the tool without any arguments to see the help documentation and a list of available commands.
