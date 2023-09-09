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
    --- get IP address (QEMU Guest Agent must be installed) of first interface
    get item 1 of (query ip of vm) -- Result: "192.168.64.9"
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

{% endraw %}
