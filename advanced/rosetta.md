---
layout: default
title: Rosetta
parent: Advanced
---
{: .label .label-green }
**macOS 13+**

Rosetta allows you to run Intel Linux executables in an Apple Silicon Linux virtual machine (using Apple Virtualization backend).

{% include toc.md %}

## Enable Rosetta
You can enable Rosetta by checking "Enable Rosetta (x86_64 Emulation)" in the wizard when setting up a Linux virtual machine. If you did not do this, you can go to the [Virtualization]({% link settings-apple/virtualization.md %}#macos-13-rosetta) tab and check "Enable Rosetta on Linux (x86_64 Emulation)".

## Mounting Rosetta Runtime
The Rosetta runtime is shared in a VirtioFS mount named `rosetta`. You can mount it with the following command:

```
$ sudo mkdir /media/rosetta
$ sudo mount -t virtiofs rosetta /media/rosetta
```

Here, we chose `/media/rosetta` as the mount point. You can use any path but you must change the rest of the commands.

### Mounting on Startup
In order to install the runtime, you need to have the share mounted at runtime. To do this, modify your `/etc/fstab` and add the following line:

```
rosetta	/media/rosetta	virtiofs	ro,nofail	0	0
```

## Enabling Rosetta
You will need the `update-binfmts` command installed which is usually part of the `binfmt-support` package. Register Rosetta as a x86_64 ELF handler:

```
$ sudo /usr/sbin/update-binfmts --install rosetta /media/rosetta/rosetta \
     --magic "\x7fELF\x02\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x3e\x00" \
     --mask "\xff\xff\xff\xff\xff\xfe\xfe\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff" \
     --credentials yes --preserve yes --fix-binary yes
```

{: .warning }
When using Rosetta in macOS 13, set the `--preserve` option to `no`. On newer versions of macOS, it should be `yes`.

{: .note }
The `magic` parameter describes the first 20 bytes of the ELF header for x86_64 binaries. The Linux kernel performs a bitwise logical AND with the first 20 bytes of a binary a user attempts to run with the mask value. If it matches the magic value, the kernel uses the registered handler as the interpreter for that binary. If the system can’t find a handler for the specified binary, it reports an error. See [Apple's documentation](https://developer.apple.com/documentation/virtualization/running_intel_binaries_in_linux_vms_with_rosetta) for more details.

## Installing Shared Libraries
In order to run x86_64 executables, you still need to install shared libraries for x86_64. The instructions vary for different distros but usually involve enabling "multiarch" or "multilib" support.

- [Ubuntu]({% link guides/ubuntu.md %})
- [Debian]({% link guides/debian.md %})

## Confirming Success

To test if your system now has binaries avaliable via the package manager you can run the following command to check if both `arm64` and `amd64` are avaiable. For example the 7-zip program:
```
sudo apt update
apt list p7zip-full
```
If you need to force install a program, you should also confirm it is an `ELF 64-bit LSB pie executable, x86-64` file.
```
sudo apt install p7zip-full:amd64
file /usr/lib/p7zip/7z
7z b
```

## Troubleshooting

Sometimes dependencies might fail to install with unconfigured changes. To troubleshoot this issue:
```
sudo apt -f install -y
```
However packages might still fail to install due to not being able to use translation or not allowed to compile through Rossetta. 

One known limitation remains with **Snap Packages** due to each package containing all their dependencies and not being able to make use of the translation.
