### Bootloader
The bootloader is the first program that will be run off of a Local Drive (HDD or SSD). How it is loaded differs depending on if it is an MBR formatted drive booted in Legacy mode, or a GPT formatted drive, booted in UEFI mode.

> _Note: It is possible to mix MBR + UEFI, or GPT + Legacy, but it is not reccomended. Doing so is bad practice, due to lack of support, risk, complexity and convention._

Bootloaders are all different, but are ultimately intended to locate and execute another more complicated system, and hand control over to it. The process of using a bootloader to bootstrap a more complicated and better equipped bootloader is very common, and is referred to as "chain-loading". Some boot loaders allow user input, and allow the user to choose between several Operating Systems (which could require more chainloading).

Bootloaders can be categorised into "stages", depending on where they are stored on the disk, which corresponds directly to their complexity:

- `Stage 1` bootloaders are located in the MBR (or VBR), and contain a few hundred bytes of executable machine code (MBR: 446 bytes, VBR: 512 bytes)
- `Stage 1.5` bootloaders are located in the "MBR Gap", or rarely have their own partition (e.g: BIOS_grub, BIOS Boot Partition)
- `Stage 2` bootloaders are located on the disk, alongside the operating system and files

##### Comparisons

Booting in UEFI can result in a completely different process, even if the Operating system ends up loaded in the same way.

For example, booting Windows (Vista onwards) in UEFI mode would load:

1) The UEFI firmware on the motherboard
2) Either `\EFI\BOOT\BOOTX64.EFI` (UEFI default location) or `\EFI\Microsoft\Boot\bootmgfw.efi` (Windows default location) on the EFI System Partition
3) The file `C:\Windows\System32\winload.efi` on the Windows Partition

Whereas booting Windows (Vista onwards) in Legacy mode would load:

1) The BIOS firmware on the motherboard
2) The MBR code, on the first sector of the drive
3) (optional) The VBR code, stored in the sector before the partition
4) The boot code `C:\$Boot` stored in the first 16 sectors (8 KiB) of the Windows Partition
5) Boot Manager `C:\bootmgr` on the Windows Partition
6) The Windows loader `C:\Windows\System32\winload.exe` on the Windows Partition
7) The Windows kernel `C:\Windows\System32\ntoskrnl.exe` on the Windows Partition

[Reference](https://docs.microsoft.com/en-us/windows/client-management/advanced-troubleshooting-boot-problems)

In windows, the exact location of a file can be found using these tools:

    fsutil fsinfo ntsfinfo c:
	fsutil volume querycluster c: <CLUSTER_NUM>
	fsutil file queryextents <FILE_PATH>
	fsutil volume filelayout <FILE_PATH>

### What partitions are used in booting?

ESP - The EFI System Partition is simply a FAT or NTFS formatted drive, which is recorded in the 

BIOS_grub

BIOS boot partition - This partition is placed at the start of the disk, and occupies the same space that the 

Windows Recovery


### What are some common bootloaders?

##### NTLDR
The legacy bootloader for Windows NT, 2000 and XP. This bootloader usually silently does its job, but can be seen and interacted with in the event of a power

##### Windows Boot Manager (Bootmgr)
The bootloader for Windows Vista, 7, 8 and 10. Like NTLDR, yo

##### GRUB


##### LILO


##### Syslinux


### How can I debug my bootloader?



### Areas for additional research
- BIOS Parameter Block (BPB)
- 



