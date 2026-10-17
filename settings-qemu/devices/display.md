---
layout: default
title: Display
parent: Devices
grand_parent: Settings (QEMU)
---
{% include toc.md %}

See [this page]({% link advanced/multiple-displays.md %}) for more details on setting up multiple displays.

## Hardware

### Emulated Display Card
This is the hardware that the guest operating system sees as the display output device.

{: .note }
The devices labeled "(GPU Supported)" support hardware accelerated rendering. You will also see an informational "GPU Acceleration Supported" toggle that is enabled when the display card supports accelerated rendering. Guest drivers are required for 3D acceleration. GPU acceleration is an experimental feature and not all applications are supported. Some 3D games and applications may crash or freeze up the VM.

### GPU Acceleration
When a "(GPU Supported)" display card is used, the following APIs can be accelerated depending on the guest drivers installed:

* **OpenGL** Linux guests with the VirGL driver in Mesa.
* **Vulkan** Linux guests with the VirtIO Venus driver in Mesa (Vulkan 1.3). See [Linux guest support]({% link guest-support/linux.md %}).
* **DirectX** Windows guests with the experimental 3D graphics driver included in the [UTM guest tools]({% link guest-support/windows.md %}).

The renderer backend as well as the Vulkan and DirectX drivers used on the host are selected globally in the preferences ([macOS]({% link preferences/macos.md %}#renderer-backend), [iOS]({% link preferences/ios.md %}#renderer-backend)). Vulkan and DirectX acceleration require the "Default" or "ANGLE (Metal)" renderer backend.

### VGA Device RAM
Certain VGA devices support the option to increase the VGA RAM in order to support larger framebuffer sizes. This is NOT VRAM and does not affect rendering performance. Most users do not need to change this. This option is only applicable to VGA display cards and will not be shown otherwise.

## Auto Resolution
This enables automatic resolution changing when the window size changes. Guest support is required. See [this page]({% link guest-support/dynamic-resolution.md %}) for more details.

## Scaling

### Upscaling/Downscaling
The scaling algorithm to use when up/downscaling. Linear scaling is good for graphical content and has anti-aliasing. Nearest neighbor is good for text and pixel art.

The default is linear for both upscaling and downscaling. When a classic computer (classic Mac OS, legacy hardware, or Windows older than 10) is created in the wizard, nearest neighbor is selected for upscaling instead because it keeps the low resolution image sharp.

### Retina Mode
When this is **disabled**, the display will be presented at the current resolution and scale that the operating system uses. This is the same resolution that all application render in and adheres to the system wide scaling settings. Typically this means the content rendered by the guest operating system is then scaled up by the host operating system before displaying it.

When this is **enabled**, UTM will tell the operating system to not scale the view and so if you are on a Hi-DPI display (sometimes called "Retina" display), the resolution reported by the guest operating system appears smaller to the host operating system. If the guest operating system supports Hi-DPI scaling, then this will result in sharper images at the cost of more memory usage and processing.

{: .note }
It is recommended that this is disabled because the host operating system can use efficient hardware scalers while the guest operating system uses software scaling which is more expensive.
