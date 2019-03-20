### What happens when my computer boots?

##### BIOS / UEFI
The "Basic Input/Output System" (BIOS), is firmware stored on the motherboard in (Read Only Memory) ROM that begins running as soon as the computer is powered on, and is responsible for creating an interface between the different computer components, so that the system can function enough to boot. The more modern version of BIOS, used by most modern motherboards is called "Unified Extensible Firmware Interface" (UEFI), but is still referred to as BIOS by many.

To seperate these terms, this article will refer to to the firmware which runs at powerup as "BIOS" (regardless of what it actually is), and the act of booting as either "Legacy Mode" or "UEFI Mode".

##### POST
One of the first tasks performed by the BIOS is the "Power On Self Test" (POST), which tests the functionality of essential components.

This often produces a series of beeps, which can be used to diagnose problems (one beep is usually success). If there is a problem in the POST, the system will shutdown (and possibly reboot).

> Here are some common reasons POST might fail:
>
> - No CPU, or incompatible CPU
> - No RAM, or RAM in wrong slots
> - Damaged components
> - Overheating (CPU fan disconnected, etc)

##### Boot Manager / Setup Utility
The Boot Manager is a the first user interface and opportunity for user interaction with the computer. The Boot Manager is typically skipped, so that the bootloader can begin as soon as possible, but it can be accessed by pressing the right key (often `DEL` or `F1`-`F12`).

The Boot Manager differs depending on the motherboard, but is where one can choose which drive to boot from, and which mode to boot them in. Additional options are frequently supported, such as system time, fan speeds, overclocking, and other advanced functionality.

##### Bootloader
The bootloader is the first program that will be run off of a Local Drive (HDD or SSD). How it is loaded differs depending on if it is an MBR formatted drive booted in Legacy mode, or a GPT formatted drive, booted in UEFI mode.

> _Note: It is technically possible to mix MBR + UEFI, or GPT + Legacy, but neither are well supported, and both are bad practice, because of risk, complexity and convention._

Bootloaders are all different, but are ultimately intended to locate and execute another more complicated system, and hand control over to it. The process of using a bootloader to bootstrap a more complicated and better equipped bootloader is very common, and is referred to as "chain-loading". Some boot loaders allow user input, and allow the user to choose between several Operating Systems (which could require more chainloading)

Bootloaders can be categorised into "stages", depending on where they are stored on the disk, which corresponds directly to their complexity.

"Stage 1" bootloaders are located in the MBR (or VBR), and contain a maximum of 446 bytes of executable machine code.

"Stage 1.5" bootloaders are located in the "MBR Gap", or rarely have their own partition (e.g: BIOS_grub, BIOS Boot Partition)

"Stage 2" bootloaders are located on the disk, alongside the operating system and files.

### What is the difference between GPT and MBR?

##### GPT

GPT formatted drives use "Blocks" as their one and only unit of measurement. The format used by all modern computers is "Logical Block Addressing" (LBA), where every block is a fixed size - 512 bytes, or 4096 bytes for 4Kn/Advanced Format (Everything after Jan 2011).

Because there are computers and applications made in the past, which aren't capable of reading GPT formatted disks, the first block is usually a "Protective MBR", which is a dummy entry, which reports that there is a single partition, of maximum size (UEFI Specification §5). This ensures that the drive is not mistakenly overridden by software which believes it to be unformatted.

The first block does not have to be a protective MBR, and can instead be a "Hybrid MBR", which exists alongside the GPT entries. This can cause issues, as an MBR partition table can ordinarily only specify 4 drives, each up to 2TiB in size, whereas GPT has easier restrictions. There are almost always conflicts if the partition table is modified in any way, as it is stored in two formats, and many applications only examine/modify one of them.

The second block contains the partition table header, and the successive 31 blocks contain partition entries. The header and partition entries are mirrored at the end of the drive, both with error checking, to reduce the chance of corruption.

Benefits of using GPT include:

- Most recent format - fully supported by all modern systems
- More partitions (4 -> 128)
- Greater partition size (2 TiB -> 8 ZiB)
- Error checking on partition table and headers

##### MBR

The MBR standard was developed in time when computers were much more primitive, so addressing was based on the physical structure of the disk being used by the computer. The three units of measurement are "Cylinders", "Heads" and "Sectors", and they are often represented in a form such as (0,0,1), which would is the first sector of addressable memory on the disk (also where the MBR sits). This is because the cylinders and heads both start counting at 0, and sectors start at 1.

> Older computers had configurations such as: (512 bytes)×(63 sectors)×(255 heads)×(1024 cylinders) = 8032.5MiB

A 512 byte area at the start of a drive (the first sector) which conforms to one of [several standards](https://en.wikipedia.org/wiki/Master_boot_record#Sector_layout), and specifies the drive partitions. The MBR can, aside from the partiton table, also contain a few hundred bytes of machine code, to be executed as a stage 1 bootloader.

Drives formatted in MBR have at least 62 sectors (31 KiB) spare. This is known as the "MBR Gap", and is often where stage 1.5 bootloaders are written to.

VBR - a 512 byte area (1 sector) at the start of a partition, which can contain code for a stage 1.5 bootloader

### What is the difference between booting in UEFI and Legacy Mode/BIOS?

Most UEFI firmware is capable of booting a drive in either UEFI Mode or legacy mode,



### What is the Compatibility Support Module (CSM)?

### What is the Boot Configuration Data (BCD)?

### What partitions are used in booting?

ESP - 

BIOS_grub

BIOS boot partition - This partition is placed at the start of the disk, and occupies the same space that the 

Windows Recovery


### What are some common bootloaders?

##### NTLDR
The legacy bootloader for Windows NT, 2000 and XP.

##### Windows Boot Manager (Bootmgr)
The bootloader for Windows Vista, 7, 8 and 10.

##### GRUB


##### LILO


##### Syslinux


### How can I debug my bootloader?


### Glossary of Acronyms

- `BIOS` Basic Input/Output System
- `POST` Power On Self Test
- `OS` Operating System
- `CPU` Central Processing Unit
- `RAM` Random Access Memory
- `ROM` Read Only Memory
- `EEPROM` Electroncially Erasable Programmable Read Only Memory
- `GRUB` Grand Unified Bootloader
- `LILO` Linux Loader
- `GPT` GUID Partition Table
- `MBR` Master Boot Record
- `VBR` Volume Boot Record
- `EFI` Extensible Firmware Interface
- `UEFI` Unified Extensible Firmware Interface
- `LBA` Logical Block Addressing
- `CSM` Compatibility Support Module
- `BCD` Boot Configuration Data
- `ESP` EFI System Partition
- `FS` File System
- `NTFS` New Technology File System (Windows default)
- `FAT` File Allocation Table

### Resources

[](https://metebalci.com/blog/a-quick-tour-of-guid-partition-table-gpt/)
[UEFI Specfification](https://uefi.org/sites/default/files/resources/UEFI%20Spec%202_6.pdf)
[Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/index.html)
