==https://social.technet.microsoft.com/Forums/exchange/en-US/4835aecb-d345-4f78-adf3-0893f06add74/uefi-vs-bios-windows-boot-process?forum=w8itproinstall==

First, you power on the machine. The machine loads the EFI/UEFI firmware.

The EFI firmware scans all connected drives/devices looking for an EFI System Partition (ESP). The ESP is defined by being FAT32 and having an EFI folder at the root. That's it. No GUID or other identification required. If it meets those two criteria, it will be automatically detected as an ESP.

The firmware then looks in that EFI folder for a *.efi file. If the OS has been previously booted/registered with the EFI firmware, then it will look for the *.efi file in a manufacturer's subdirectory of the EFI folder, ie "EFI\Microsoft". If the EFI firmware does not have any record of an OS, it will try to load "EFI\Boot\bootx64.efi". Not sure where it goes in the case that bootx64.efi is loaded.

However, if the firmware manages to load "EFI\Microsoft\boot\bootmgrfw.efi", the Windows bootloader, bootmgrfw.efi will look for a BCD file in its same directory. That BCD file will enumerate all the Windows installations on the disk. It will either present a menu, or load the default Windows OS.

When bootmgrfw.efi loads Windows, it looks in the root directory given by the BCD file. In this case, it'll be C:\Windows. Inside C:\Windows, we have "winload.exe" or maybe "winload.efi". One of those gets loaded and loads the kernel, etc. This is when the OS officially takes over.


So, to answer my original question, if you want to use GPT/UEFI, you need an ESP with the EFI folder and associated *.efi and BCD files. Don't need anything in C:\. If you want to use MBR/BIOS, you do not need an extra partition, but you need BOOTMGR and possibly a BCD file, located in C:\.

==https://askubuntu.com/questions/778663/what-is-the-difference-between-windows-uefi-bootmgfw-efi-and-windows-uefi-bkpboo==

The bkpbootx64.efi is a backup regularly created by Boot-Repair. With Windows the bootx64.efi is just really a copy of Windows bootmgfw.efi. And bootx64.efi is a fallback or hard drive boot entry in UEFI.

But Boot-Repair with its 'Use the standard EFI file` in advanced options creates the bkpbootx64.efi and makes bootx64.efi a copy of shimx64.efi so fallback or hard drive boot entry in UEFI really boots grub not Windows.

====