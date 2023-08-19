---
layout: default
title: Remote Control
parent: Advanced
---
The URL scheme `utm` is associated with the UTM app. To launch or bring to foreground UTM, open the URL `utm://` (for example Safari, Shortcuts "Open URL" action, Automator).

## Supported Commands

Commands marked ⚠️ can result in data loss or corruption in the guest VM, as the VM is shut down improperly.

| Command | Parameter(s) | Result | Example |
|-|-|-|-|
| `start` | `name` of the VM | The VM with the provided name is started, if it's not already started. | `utm://start?name=Ubuntu%2020.04` |
| `stop` | `name` of the VM | The VM with the provided name is stopped immediately. ⚠️ | `utm://stop?name=Ubuntu%2020.04` |
| `restart` | `name` of the VM | The VM with the provided name is stopped immediately, then started again. ⚠️ | `utm://restart?name=Ubuntu%2020.04` |
| `pause` | `name` of the VM | The VM with the provided name is paused. (not supported for all VMs) | `utm://pause?name=Ubuntu%2020.04` |
| `resume` | `name` of the VM | The VM with the provided name is resumed (un-paused). | `utm://resume?name=Ubuntu%2020.04` |
| `sendText` | `name` of the VM and text to be typed in the VM | The VM with the provided name receives the supplied text as keyboard input. | `utm://sendText?name=Ubuntu%2020.04&text=abcdef` (types "abcdef" in the VM) |
| `click` | `name` of the VM, `x` and `y` position to click, optional: mouse `button` to click (left/middle/right, default left) | The VM with the provided name receives a mouse click down and up event at the specified pixel location. | `utm://click?name=Ubuntu%2020.04&x=10&y=125&button=right` (right clicks at (10/125) in the VM) |
| `downloadVM` | `url` to the VM, must be ZIP file of a `.utm` package (URL must contain `.zip`). | Downloads the ZIP file (progress shown in UTM with cancel button), then extracts and imports the contained `.utm` file. | `utm://downloadVM?url=https%3A%2F%2Fchrisp.cafe%2FUTM%2FXP.zip` (downloads a VM template for Windows XP) |

Note on the `sendText` action: you can send [ASCII Control Codes](https://jkorpela.fi/chars/c0.html) to the VM, here are some common ones:
- Esc is `%1b`
- Delete (backspace) is `%08`
- Tab is `%09`
- Enter is `%0D`

## URL Parameter Encoding

The parameters like `name`, `text`, and `url` need to be URL encoded so they are received correctly. For example, if the VM "Ubuntu 20.04" should be addressed, the name parameter is "Ubuntu%2020.04". If you're using Shortcuts "Open URL" action, this is done automatically. Otherwise you can use apps like [Boop](https://apps.apple.com/app/id1518425043) or websites like [DuckDuckGo](https://duckduckgo.com/?q=URL+encode+Ubuntu+20.04&t=h_&ia=answer) or [Dan's Tools URL Encode Decode](https://www.url-encode-decode.com) to perform the encoding.

## UTM Automation using Shortcuts (macOS 12 Monterey and iOS)

![Shortcuts screenshot. Description below.](https://user-images.githubusercontent.com/12073163/180662436-b888ae8b-436c-4504-8bd2-97ed6b09eb6f.jpg)

1. URL action with the parameter utm://start?name=Ubuntu 20.04
2. Open URLs action

[Download this shortcut](https://www.icloud.com/shortcuts/694ce443e0af409799805a903824b9ae).

## Start a VM automatically when you log in (macOS 12 Monterey)

First, create a Shortcut to launch the VM as shown above. Then, select the shortcut in the list and choose File → Add to Dock.

![UTM-shortcut-add-to-dock](https://user-images.githubusercontent.com/12073163/140542990-f8014e67-7835-4ed2-9629-666ae8b55573.jpg)

The Shortcut will appear in your Dock. Hold down the ⌘ (cmd) key while clicking on the icon in the Dock to reveal the Shortcut file in Finder. A Finder window will open in the folder ~/Applications/. Add the Shortcut file to your [Login Items](https://support.apple.com/guide/mac-help/open-items-automatically-when-you-log-in-mh15189/mac) (System Preferences → Users and Groups → Login Items):

![UTM-start-vm-at-login-shortcuts](https://user-images.githubusercontent.com/12073163/140543255-c3aaa1a3-81c0-4586-a4f8-1f2fb30c430a.jpg)

To stop the VM from starting at login, open the Login Items page again, select the Shortcut in the list, and press the minus button (-).

## UTM for Mac Automation using Automator (macOS 11 Big Sur)

Here is an example Workflow created in [Automator](https://support.apple.com/guide/automator/welcome/mac):

![Automator screenshot](https://user-images.githubusercontent.com/12073163/137601163-cc3caa68-f3e9-43bc-846c-85b800709971.jpg)

1. Get Specified Text: utm://start?name=Ubuntu%2020.04
2. Extract URLs from Text
3. Display Webpages

## Start a VM automatically when you log in (macOS 11 Big Sur)

To start a VM automatically when you log in to your Mac, create an Automator workflow like above to start the VM you want. Then add it to your [Login Items](https://support.apple.com/guide/mac-help/open-items-automatically-when-you-log-in-mh15189/11.0/mac/11.0) (System Preferences → Users and Groups → Login Items).

![An Automator document is dragged into the System Preferences app. The System Preferences is showing the Users & Groups pane, Login Items section. The Automator document ends up in the list of Login Items.](https://user-images.githubusercontent.com/12073163/137601677-eade9d8f-e503-4db9-bb79-3aa3023064c9.jpg)

