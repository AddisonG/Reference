# BIOS Firmware

The "Basic Input/Output System" (BIOS), is firmware stored on the motherboard in (Read Only Memory) ROM that begins running as soon as the computer is powered on, and is responsible for creating a basic interface between the computer components, and running the code in the MBR of the drive that is to be booted from.

BIOS is implemented differently by each company, but are designed to be compatible with the IBM PC's proprietary BIOS, which is where the de-facto standard comes from.

No new motherboard (~post 2013) runs BIOS anymore - They all run firmware that conforms to the UEFI standard, or occasionally another piece of firmware such as [coreboot](https://www.coreboot.org).

### Issues:

##### De-facto Standard

BIOS is a de-facto standard, and still works around restrictions that were only an issue in the 1980's.

##### Runs Code in Real Mode

BIOS and all legacy bootloaders run code in "Real Mode" (not "Protected Mode") meaning that any operation can be performed, without restrictions, by the CPU. 

>This is risky, as corrupted code can potentially overwrite or delete data, and malicious code can be inserted into bootloaders that runs with the highest permissions, and can access and modify any application, file or network traffic, without ever being detected.

### Booting in Legacy Mode
Most UEFI firmware is capable of booting a drive in either UEFI Mode or legacy mode (using the CSM), but older motherboards are only capable of booting using BIOS.
