---
layout: default
title: System
parent: Settings (QEMU)
---
{% include toc.md %}

## Architecture
This is the CPU architecture that should be emulated by UTM. The list is determined by the architectures that QEMU supports.

{: .note }
Virtualization requires the guest architecture to match the host. That means x86_64 for Intel Macs and aarch64 for Apple Silicon. If the guest architecture does not match the host, virtualization will not be used even if enabled in the QEMU settings.

**iOS**{: .label .label-blue } UTM SE supports a limited subset of architectures. Currently these are: aarch64, i386, ppc, ppc64, riscv32, riscv64, and x86_64

## System
QEMU supports multiple target systems for each architecture. In most cases, you should leave the default option for the best results. One exception is when emulating an older PC (x86_64 or i386), `Standard PC (i440FX + PIIX, 1996) (alias of...` should be used instead of the default (2009 model). This is known to work better for older Windows and DOS emulation.

## Memory
For the best performance, the amount of memory should not exceed the amount of memory in your system.

**iOS**{: .label .label-blue } Non-jailbroken iOS devices are limited by the operating system on the amount of memory that can be allocated. This limit is typically around 1/2 of the size of the device's physical memory.

## CPU
The CPU model emulated by QEMU can be specified but should be left at the default value except for advanced use cases.

The number of cores can be specified. If left blank or set to 0, a default number will be chosen. This default is the number of performance cores on Apple Silicon or the number of physical cores on Intel. When emulating strong-on-weak systems, the default number of cores will always be 1.

"Force multicore" must be selected when attempting to emulate multiple cores of a strong memory system on a weak memory system (strong-on-weak). A typical example of strong-on-weak is attempting to emulate x86_64/i386 on an ARM host. In these cases, QEMU does not guarantee the correctness of the emulation. You must also manually specify the number of cores when forcing multicore.

## JIT Cache
This applies only for emulation. The JIT cache allows for translated code to be cached for faster execution. It is analogous to L2 cache in hardware. Although a larger cache size is usually better, there is diminishing returns when it is too large. The default value is 1/4 of the memory size configured above. The JIT cache is allocated separately from the guest memory and the size configured above does not include the JIT cache size.

**iOS**{: .label .label-blue } On JIT supported builds the operating system will double count the JIT cache size when determining if the application exceeded the system limit. Therefore, if you run into low memory issues, you can try lowering the JIT cache size first.
