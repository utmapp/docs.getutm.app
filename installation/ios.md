---
layout: default
title: iOS
parent: Installation
nav_order: 1
---
{: .label .label-blue }
**iOS**

{% include toc.md %}

UTM works on all devices running iOS 11 or higher if jailbroken. UTM can also be run [semi-tethered][9] on non-jailbroken devices. UTM runs untethered on some non-jailbroken devices with limited compatibility depending on your iOS version and device processor. See the list below for more details.

[Download from GitHub](https://github.com/utmapp/UTM/releases/latest){: .btn .btn-blue }

## Non-Jailbroken Devices

**If you are running iOS 11, 12, or 13**: UTM does not require a jailbreak to use, but you must sideload it. If you are new to sideloading, it is a way to use a developer's certificate to load unapproved apps on a non-jailbroken iOS device. There are a few limitations to sideloading:

* Free developer accounts must re-sign every 7 days
* Paid developer accounts must re-sign every 1 year

{: .note }
The last version of UTM that supports iOS 11-13 is [v3.2.4](https://github.com/utmapp/UTM/releases/tag/v3.2.4).

**If you are running iOS 14.2, 14.3**: UTM works with sideloading (non-jailbroken) if your device has an Apple A12 chip or newer. Otherwise, keep reading.

**If you are running iOS 14.0, 14.1, 14.4, or higher**: UTM works if you are jailbroken or [semi-tethered with Jitterbug][9], AltJIT, or [Jitstreamer][10]. "Semi-tethered" means either tethered to a Mac/PC, to another iOS device with Wifi sharing, or to itself (one iOS device running both Jitterbug/AltJIT and UTM) through a on-device VPN profile.

### AltStore Repository

Note: at this time, 3rd party repos require a beta of AltStore which is available only to the developer's Patreon supporters. When installing from the repository, you can recieve update prompts from AltStore.

1. Install [AltStore][4]
2. Add the source: [https://alt.getutm.app][5]
3. Download UTM from AltStore

### AltStore Sideloading

For non beta-testers, the public release of AltStore lacks the ability to add repositories and check updates but can still manage re-signing automatically.

1. Install [AltStore][4]
2. Download the [latest IPA release][1] on your device
3. Open the IPA with AltStore

### Other Methods

There are many "cloud" signing services do **not** work with UTM because they use the wrong kind of signing certificate. If you get a crash or a black screen while trying to start a VM, it is likely that your signing certificate was invalid.

You can check if you have the right signing certificate by going to `Settings -> General -> Profiles & Device Management`. If the certificate used for signing UTM is listed under `Developer App`, then it is good. If it is listed under anything else such as `Enterprise App`, then it is the wrong certificate.

{: .note }
UTM SE does not support JIT (will run much slower) but is compatible with all signing services.

## TrollStore

If your device runs [TrollStore][11], then UTM can support additional features such as USB sharing and virtualization (currently limited to M1 iPads). You can install via TrollStore by downloading the TrollStore compatible IPA (UTM.HV.ipa) on your device and opening it with TrollStore.

{: .note }
You cannot install the normal IPA (UTM.ipa) because it includes the `dynamic-codesigning` entitlements which TrollStore does not support.

## Jailbroken Devices

UTM requires AppSync Unified which can be found on [Karen's Repo][8]. You need to add both repositories to your package manager (Cydia, Sileo, Zebra, etc.) to install UTM.

1. Add [https://cydia.akemi.ai/][8] for AppSync Unified.
2. Add [https://cydia.getutm.app/][7] for UTM.

## Summary

| File | Description | Installation | JIT | Hypervisor | USB |
|------|------------|--------------|-----|-----------|-----|
| [UTM.deb](https://github.com/utmapp/UTM/releases/latest/download/UTM.deb) | Jailbroken iOS version | Open in Cydia, dpkg, or Sileo | Yes | Yes(1) | Yes |
| [UTM.ipa](https://github.com/utmapp/UTM/releases/latest/download/UTM.ipa) | Non-jailbroken iOS version (sideloading) | AltStore, etc (see guide) | Yes(2) | No | No |
| [UTM.HV.ipa](https://github.com/utmapp/UTM/releases/latest/download/UTM.HV.ipa) | Non-jailbroken iOS version (TrollStore) | TrollStore | Yes | Yes(1) | Yes |
| [UTM.SE.ipa](https://github.com/utmapp/UTM/releases/latest/download/UTM.SE.ipa) | Non-jailbroken iOS version (sideloading) | AltStore, enterprise signing, etc | No | No | No |

1. Hypervisor on iOS requires an M1 iPad.
2. Enabling JIT may require a separate JIT enabler such as [Jitterbug][9] or [Jitstreamer][10].

  [1]: https://github.com/utmapp/UTM/releases/latest
  [2]: https://dantheman827.github.io/ios-app-signer/
  [3]: https://discord.gg/UV2RUgD
  [4]: https://altstore.io
  [5]: altstore://source?url=https://alt.getutm.app
  [6]: https://repo.dynastic.co/package/altdaemon
  [7]: cydia://url/https://cydia.saurik.com/api/share#?source=https://cydia.getutm.app/
  [8]: cydia://url/https://cydia.saurik.com/api/share#?source=https://cydia.akemi.ai/
  [9]: https://github.com/osy/Jitterbug
  [10]: https://github.com/jkcoxson/JitStreamer
  [11]: https://github.com/opa334/TrollStore