---
layout: default
title: Display
parent: Devices
grand_parent: Settings (Apple)
---
{: .label .label-green }
**macOS**

{% include toc.md %}

## Resolution
The resolution used by the guest to render graphics.

## HiDPI (Retina)
If **disabled**, native scaling performed by the host operating system will be performed. If **enabled**, the resolution seen by the guest will be the value specified above multiplied by the scale factor of the current display. For example, a "retina" display is typically 2x or 3x the resolution. This will allow the guest to do its own HiDPI rendering and scaling. This is discouraged because host scaling is usually more efficient.
