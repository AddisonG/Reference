# GRUB
[Archlinux Grub](https://wiki.archlinux.org/index.php/GRUB)
[Archlinux Grub EFI Examples](https://wiki.archlinux.org/index.php/GRUB/EFI_examples)

# Fixing GRUB on BIOS/MBR mode

Try using

    bootrec.exe /fixboot
	bootrec.exe /RebuildBcd

This will wipe out GRUB:

    bootrec.exe /Fixmbr


GRUB Entry for Windows Vista/7/8/10:

	if [ "${grub_platform}" == "pc" ]; then
		menuentry "Microsoft Windows Vista/7/8/8.1/10 BIOS/MBR" {
			insmod part_msdos
			insmod ntfs
			insmod ntldr     
			search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 XXXXXXXXXXXXXXXX
			ntldr /bootmgr
		}
	fi

# Fixing GRUB on UEFI/GPT mode

GRUB Entry for Windows Vista/7/8/10:

	if [ "${grub_platform}" == "efi" ]; then
		menuentry "Microsoft Windows Vista/7/8/8.1 UEFI/GPT" {
			insmod part_gpt
			insmod fat
			insmod chain
			search --no-floppy --fs-uuid --set=root $hints_string $fs_uuid
			chainloader /EFI/Microsoft/Boot/bootmgfw.efi
		}
	fi

