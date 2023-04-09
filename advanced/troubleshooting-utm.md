---
layout: default
title: Troubleshooting UTM and System Errors
parent: Advanced
---
Should I be troubleshooting UTM?

If you encounter either a crash or an error popup while using UTM, you should begin by Troubleshooting the virtual machine you are trying to use. You should continue reading this document if the problem you are experiencing is not related to a specific VM, or it happens before you start a VM.

System Log
What is a System Log?
This is a large amount of text that contains messages from the software running on a computer. It contains clues as to what is happening and especially, what might have gone wrong.

In some cases, this file might include identifying or personal information, for example IP addresses of your computer and/or other devices on your LAN, or information entered in applications currently running on your computer at the time of the log file creation. If you are uncomfortable with sharing this information publicly (here online), you can quit all other applications while collecting the log, and obfuscate any remaining personal information by hand before you upload the file.

When do I not need a system log?
If the UTM app does not crash or show an error before a VM starts, you likely do not need a system log. Check the Debug Log first. If it does not show any error, get the System Log.

How to get macOS System Log for UTM troubleshooting?
Quit UTM if it is opened.
Open Console app, click Start streaming.
In the Console app search box type "UTM" and press return, then click on the grey "any" dropdown and choose "process". The app should show no results (if there are any, click Clear).
Open UTM and attempt to start a VM (keep going until the error popup or crash)
Quit UTM
In Console app, click one of the lines of activity (center of the window), then in the Menu Bar, choose Edit => Select All and Edit => Copy.
Open TextEdit app, choose File => New, then Format => Make Plain Text.
Choose Edit => Paste, then File => Save
In the "Save As:" field, type UTM-System-Log.log, in the "Where" field choose Desktop, then click Save.
If you are retrieving the log for a GitHub issue, open the issue page in your web browser and attach the UTM-System-Log.log file (in a new comment).

How to read macOS System Log
Error or warning messages are common hints to app or system problems. The log file is made of many lines of text. The lines might include information, warnings and errors.

The lines are structured similar to this:

TIMESTAMP  PROCESS    MESSAGE
For example:

00:00:08.299247    UTM    container_create_or_lookup_for_platform: success
TIMESTAMP means when was the text produced by the system, PROCESS means which app sent the text, and MESSAGE is the text from the app.

In the above example, the MESSAGE is container_create_or_lookup_for_platform: success. While produced by UTM (according to the PROCESS part), it is in fact a macOS system-related message that occurs most of the time an app is launched. The : success part means it is not an error message.

Usually, error messages include one of the words "error", "fail", "crash", "timeout", "hang", "panic", or "obsolete". Some messages might not include one of these words, but they are likely phrased in a negative way, for example "Couldn't read values".

If the text in a certain line does not contain these words, it might not be an error and instead it could be a warning or information. Most of the lines in the System Log are information to indicate that things are happening.


