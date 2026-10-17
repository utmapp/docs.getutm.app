---
layout: default
title: Cheat Sheet
parent: Scripting
---
{: .label .label-green }
**macOS**

{% include toc.md %}

{% raw %}

## List and find VMs

```applescript
tell application "UTM"
    --- listing virtual machines
    set vms to virtual machines
    --- get vm by name
    set vm to virtual machine named "Ubuntu"
    --- get vm by id
    set vm to virtual machine id "5D419106-2824-4FED-BFE1-24A7F7E253D8"
end tell
```

## Control VMs

```applescript
tell application "UTM"
    set vm to virtual machine named "Ubuntu"
    --- start a vm
    start vm
    --- start a vm in disposable mode
    start vm without saving
    --- pause a vm
    suspend vm
    --- pause a vm and attempt to save the state (when supported)
    suspend vm with saving
    --- stop a vm
    stop vm
    --- force shutdown a vm
    stop vm by force
    --- kill the vm process
    stop vm by kill
end tell
```

## Creating a VM

```applescript
tell application "UTM"
    --- specify a boot ISO
    set iso to POSIX file "/path/to/ubuntu.iso"
    --- create a new QEMU VM for ARM64 with a single 64GiB drive
    set vm to make new virtual machine with properties {backend:qemu, configuration:{name:"QEMU ARM64", architecture:"aarch64", drives:{{removable:true, source:iso}, {guest size:65536}}}}
    --- note the default options for a new VM is no display, one PTTY serial port, and one shared network
    --- duplicate an existing VM and disable hypervisor in the duplicate
    duplicate vm with properties {configuration:{name:"Duplicate QEMU ARM64", hypervisor:false}}
    --- create an Apple VM for booting Linux (only supported on macOS 13+)
    make new virtual machine with properties {backend:apple, configuration:{name:"Apple Linux", drives:{{removable:true, source:iso}, {guest size:65536}}}}
end tell
```

## Creating a macOS VM

Only supported on Apple Silicon. Automatically setting up the user account on first boot requires macOS 27 or later on both the host and the guest.

```applescript
tell application "UTM"
    --- specify the IPSW to install from
    set ipsw to POSIX file "/path/to/UniversalMac_Restore.ipsw"
    --- create an Apple VM for macOS with a 128GiB drive
    set vm to make new virtual machine with properties {backend:apple, configuration:{name:"macOS", os:macOS, macRecoveryIpsw:ipsw, memory:8192, drives:{{guest size:131072}}}}
    --- install macOS (ALL DATA ON THE PRIMARY DRIVE WILL BE ERASED WITHOUT CONFIRMATION!)
    install vm
    --- wait until the installation is complete
    repeat
        set p to query install vm
        if not installing of p then exit repeat
        delay 10
    end repeat
    --- on the first start, create an account, log in automatically, and turn on Remote Login (SSH)
    start vm provisioning {username:"user", password:"password", automatic login:true, remote login:true}
end tell
```

## Deleting a VM

```applescript
tell application "UTM"
    --- delete a vm and all its data (NO CONFIRMATION WILL BE GIVEN!)
    delete virtual machine named "Ubuntu"
end tell
```

## Status and information

```applescript
tell application "UTM"
    set vm to virtual machine named "Ubuntu"
    start vm
    --- wait until vm is started
    repeat
        if status of vm is started then exit repeat
    end repeat
    --- get status
    get status of vm --- Result: "started"
    --- get serial port address
    get address of first serial port of vm --- Result: "/dev/ttys011"
    --- get IP address of first interface (for QEMU, the QEMU Guest Agent must be installed)
    get item 1 of (query ip of vm) -- Result: "192.168.64.9"
end tell
```

## Snapshots

QEMU virtual machines are supported on all versions of macOS. Apple virtual machines require macOS 27 or later and must be stopped for every operation except delete.

```applescript
tell application "UTM"
    set vm to virtual machine named "Ubuntu"
    --- list snapshots (newest first)
    get name of every snapshot of vm
    --- save the current state as a new snapshot
    set snap to create snapshot vm named "Before update"
    --- get information about a snapshot
    get {creation date, size, includes running state} of snap
    --- rename a snapshot
    set name of snap to "Clean install"
    --- find a snapshot by name
    set snap to snapshot "Clean install" of vm
    --- replace the current state of the vm with the snapshot
    restore snap
    --- replace the snapshot with the current state of the vm
    overwrite snap
    --- delete a snapshot (NO CONFIRMATION WILL BE GIVEN!)
    delete snapshot snap
    --- discard the suspended state so the vm starts up normally
    discard saved state vm
    --- look for snapshots made by other tools (such as qemu-img)
    scan snapshots vm
end tell
```

## Configuration

```applescript
tell application "UTM"
    set vm to virtual machine named "Ubuntu"
    set config to configuration of vm
    --- get architecture of the vm
    get architecture of config
    --- set a single setting
    set hypervisor of config to false
    --- set the ISO of a removable drive
    set iso to POSIX file "/path/to/ubuntu.iso"
    set i to id of item 1 of drives of config
    set item 1 of drives of config to {id:i, source:iso}
    --- save the configuration (VM must be stopped)
    update configuration of vm with config
    --- reload the configuration from disk if the .utm package was modified by another tool (VM must be stopped)
    reload configuration vm
end tell
```

## Network configuration

```applescript
tell application "UTM"
    --- change the emulated VLAN of a QEMU VM in shared network mode
    set vm to virtual machine named "Ubuntu"
    set config to configuration of vm
    set nic to item 1 of network interfaces of config
    set vlan guest address of nic to "192.168.100.0/24"
    set vlan dhcp start address of nic to "192.168.100.10"
    set vlan dhcp end address of nic to "192.168.100.100"
    --- prevent the guest from accessing the host
    set isolate from host of nic to true
    set item 1 of network interfaces of config to nic
    update configuration of vm with config
    --- put an Apple VM on a NAT network shared with other VMs (macOS 26+)
    set vm to virtual machine named "Apple Linux"
    set config to configuration of vm
    set mode of item 1 of network interfaces of config to nat network
    update configuration of vm with config
end tell
```

## Read/write files

```applescript
tell application "UTM"
    --- QEMU guest agent must be installed
    set vm to virtual machine named "Ubuntu"
    --- read a text file at random offsets
    tell (open file of vm at "/tmp/hello" for reading)
        --- read two characters from the start
        read for length 2 without closing
        --- read two characters from the end
        read at offset -2 from end position for length 2 without closing
        -- remember to close the file if read without closing
        close -- remember to close the file if read without closing
    end tell
    --- write data to a binary file
    tell (open file of vm at "/tmp/hello" for writing)
        write with data "njq81XwLTBF2eOzTuMZfrg==" with base64 encoding without closing
        close
    end tell
    --- copy file from guest to host
    set output to POSIX file "/path/to/output"
    pull of (open file of vm at "/tmp/hello") to output
    --- copy file from host to guest
    set input to POSIX file "/path/to/input"
    push of (open file of vm at "/tmp/hello" for writing) from input
end tell
```

## Execute commands

```applescript
tell application "UTM"
    --- QEMU guest agent must be installed
    set vm to virtual machine named "Ubuntu"
    --- run a shell command
    execute of vm at "wget" with arguments {"http://example.com"}
    --- run a shell command and capture the output
    tell (execute of vm at "ls" with arguments {"-l", "/"} with output capturing)
        --- wait until execution is complete
        repeat
            set res to get result
            if exited of res then exit repeat
        end repeat
        --- fetch stdout as text
        get output text of res
        --- fetch stdout as base64 data
        get output data of res
    end tell
end tell
```

## USB Devices

USB devices can be connected to QEMU VMs with USB sharing enabled and to Apple VMs on macOS 27 or later. For Apple VMs, the device must first be [assigned to UTM]({% endraw %}{% link guest-support/sharing/usb.md %}{% raw %}).

```applescript
tell application "UTM"
    --- get first USB device connected to the host
	set device to first usb device
    --- get the VM that is running
	set vm to virtual machine named "Ubuntu"
    --- connect the device to the VM
    connect device to vm
    --- disconnect the device from the VM
	disconnect device
end tell
```

## Input automation

```applescript
tell application "UTM"
	set vm to virtual machine named "Ubuntu"
	--- send 'hello' as a sequence of raw PC AT scan codes (make + break)
	input scan code of vm codes {35, 163, 18, 146, 38, 166, 38, 166, 24, 152}
	--- send 'HELLO' as a string of characters with shift modifier
	input keystroke of vm text "hello" with modifiers shift
	--- send a left mouse click at (50, 50) of the primary display
	input mouse click of vm at {50, 50} with mouse button left
end tell
```

{% endraw %}
