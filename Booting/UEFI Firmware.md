##### UEFI Mode

The modern firmware used by all recent motherboards is called "Unified Extensible Firmware Interface" (UEFI), but is still wrongly referred to as BIOS by many, as it is far more widely understood.

Only modern motherboards have the firmware required to perform a UEFI boot. In the past, there were competing standards, rapidly advancing technologies, and the resources required to boot from the motherboard weren't feasible.

Nowadays, the UEFI firmware simply searches the drive to boot from for a partition of a specific type - An EFI System Partition (ESP). These dedicated partitions, usually between 100 to 550MiB, contain complex bootloaders of any size, with minimal restrictions on file size, memory, or access to drive addresses.

Many bootloaders allow interfaces that 
