### MBR

The MBR standard was developed in time when computers were much more primitive, so addressing was based on the physical structure of the disk being used by the computer. The three units of measurement are "Cylinders", "Heads" and "Sectors" (CHS), and they are often represented in a form such as (0,0,1), which would is the first sector of addressable memory on the disk (also where the MBR sits). This is because the cylinders and heads both start counting at 0, and sectors start at 1.

> Older computers had configurations such as: (512 bytes)×(63 sectors)×(255 heads)×(1024 cylinders) = 8032.5MiB

A 512 byte area at the start of a drive (the first sector) which conforms to one of [several de-facto standards](https://en.wikipedia.org/wiki/Master_boot_record#Sector_layout), and specifies the drive partitions. The MBR can, aside from the partiton table, also contain a few hundred bytes of machine code, to be executed as a stage 1 bootloader by the BIOS firmware.

Drives formatted in MBR have at least 62 sectors (31 KiB) spare, as DOS used to require that partitions started on the Cylinder Boundary. This space is known as the "MBR Gap", and is often where stage 1.5 bootloaders are written to.

The "Volume Boot Record" or "Partition Boot Record" (VBR / PBR) is a, or a 512 byte area (1 sector) at the start of a partition, which can contain code for a stage 1.5 bootloader.
