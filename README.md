# z-vm-autoddr
Script to automate DDRing for DUMP and RESTORE using z/VM RAMDISK

This script formats a disk for use in CMS and dumps all marked DASDs
to files onto that disk. This is useful to consolidate backups of
many small DASDs onto larger SCSI disks for example.

A listing called `DASD LIST` is created on the disk as well as a
restore script called `RESTORE EXEC` that will DDR in the opposite
direction.

## Configuration

Example Hercules configuration:

```
# [...]
# 0A99 3390 zos21/S1IMC1.64 ro cu=3990-6 # DUMP: S1IMC1
# 0A9A 3390 zos21/S1IMD1.64 ro cu=3990-6 # DUMP: S1IMD1
# 0A9B 3390 zos21/S1DIS1.64 ro cu=3990-6 # DUMP: S1DIS1
# [...]
# 0200 9336 zv2r1.hba
```

This will dump disks 0A99 through 0A9B to the files `0A99 S1IMC1`
and so on.

## Usage

The script uses s3270, part of the x3270 suite to automate command
input to an IPLed z/VM RAMDISK. Simply connect the script to an IPL'd
z/VM RAMDISK and it will take it from there. The system will shut down
after the dump has completed.

```
# After IPL of z/VM RAMDISK
./autoddr localhost:3270 zvm.conf ZV2R1 | s3270
```
