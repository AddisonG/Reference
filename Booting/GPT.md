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
