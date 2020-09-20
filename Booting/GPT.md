### GPT

GPT formatted drives use "Blocks" as their one and only unit of measurement. The format used by all modern computers is "Logical Block Addressing" (LBA), where every block is a fixed size - 512 bytes, or 4096 bytes for 4Kn/Advanced Format (Everything after Jan 2011).

Because there are computers and applications made in the past, which aren't capable of reading GPT formatted disks, the first block is usually a "Protective MBR", which is a 512 byte dummy entry, which reports that there is a single partition, of maximum size (UEFI Specification §5). This ensures that the drive is not accidentally overridden after being mistaken as an unformatted or corrupt drive.

##### Hybrid MBR
The first block does not *have* to be a protective MBR. It can instead be a "Hybrid MBR", which exists alongside the GPT entries. This can cause issues, as an MBR partition table can ordinarily only specify 4 drives, each up to 2TiB in size, whereas GPT has easier restrictions. There are almost always conflicts if the partition table is modified in any way, as it is stored in two formats, and many applications only examine/modify one of them.

The second block contains the partition table header, and the successive 31 blocks contain partition entries. The header and partition entries are mirrored at the end of the drive, both with error checking, to reduce the chance of corruption.

Benefits of using GPT include:

- Most recent format - fully supported by all modern systems
- More partitions (4 -> 128)
- Greater partition size (2 TiB -> 8 ZiB)
- Error checking on partition table and headers

# Start Sectors
LBA 0 is reserved for the Protective MBR.
LBA 1 is the GPT Header.
LBA 2-33* are the GPT Partition Entries (128 bytes each).
LBA 34 is the first useable sector.

*The GPT can be modified to contain less partition entries. E.g: If there was only room for 24 partition entires, then the first (optimal) useable sector would be 8.

To align to 4096-byte alignments, starting on a multiple of 8 is strongly recommended unless you are positive that your disk is using physical sectors of 512 bytes. Thus, 40 is the best first sector for a standard setup.
Unfortunately, a lot of utilities assume that 2048 is the first sector, and break VERY easily.


http://jdebp.eu./FGA/disc-partition-alignment.html
http://rodsbooks.com./gdisk/
https://superuser.com/questions/1345844/why-disk-partitions-start-at-sector-2048
