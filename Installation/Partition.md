# Identifying the disk
Run:
```bash
lsblk
```
Example of this output:
```bash

NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0         7:0    0  700M  1 loop /run/archiso/airootfs
sda           8:0    1   16G  0 disk
├─sda1        8:1    1   16G  0 part /run/archiso/bootmnt
nvme0n1     259:0    0  512G  0 disk
├─nvme0n1p1 259:1    0   300M 0 part
├─nvme0n1p2 259:2    0   100G 0 part
```
Let me explain what does each part means
## Loop devices
loop0 is the live Arch ISO system,ignore this.

## USB drive(your bootable pendrive)
•sda
•RM = 1 means removable device
•Ignore this

## Your actual disk

- nvme0n1(SSD), sda(SATA SSD) and sdb(SATA HDD)
How to identity:
• Larger size (256GB, 512GB, etc)
• RM = 0 (not removable)
This is the disk where Arch will be installed.

# Partition the disk
The next step, we will have to partition the disk.
For that we will use a utility called 'cfdisk'
 
Type this:
```bash
cfdisk /dev/nvme0n1 //Replace nvme0n1 with your disk
```
Inside cfdisk will be see something like this:
