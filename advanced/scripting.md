---
layout: default
title: Scripting
parent: Advanced
---
{: .label .label-green }
**macOS**

{% include toc.md %}

UTM provides power users with access to an AppleScript bridge interface paired with a command line interface. Note that not all features are currently supported in the scripting interface and feedback is welcome on what should be added.

## AppleScript
Details on the verbs and nouns available in the scripting interface can be found in the AppleScript dictionary. To browse the dictionary:

1. Open "Script Editor" (found in Applications → Utilities)
2. In the menu bar choose File → Open Dictionary... (or Shift+Cmd+O)
3. Select UTM from the list of applications

## Command Line Interface
The CLI tool is a wrapper around the AppleScript interface and shares the same functionality. It can be found at:

```
/Applications/UTM.app/Contents/MacOS/utmctl
```

It is recommended you "install" this by creating a symbolic link to your `bin` directory:

```
$ sudo ln -sf /Applications/UTM.app/Contents/MacOS/utmctl /usr/local/bin
```

Run the tool without any arguments to see the help documentation and a list of available commands.
