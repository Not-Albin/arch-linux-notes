# Format the partition

Next step to do after creating the partition is to format it.
Carefully, this step requires to format the partition make sure to double check if you are formatting thr correct disk.

## Create an Ext4 file system on your root partition
```bash
mkfs.ext4 /dev/sda3
```
Replace disk with your root partition.

## Next initialize your swap partition.
```bash
mkswap /dev/sda2
```
## After that you have to format your EFI file partition.
```bash
mkfs.fat -F 32 /dev/sda1
```
That is for the disk formatting.

Next we have to mount these partition with our linux file system.

# Mount the file system

First mount the root volume to /mnt
```bash
mount /dev/sda3 /mnt
```
Here we mounted our root partition for core linux system.

Then we have to mount the EFI partition.
```bash
mkdir -P /mnt/boot
mount /dev/sda1 /mnt/boot
```
Here we mounted our EFI partition to the boot loader.

After that we have to turn on the swap partition.
```bash
swapon /dev/sda2
```
Last step, mount the home partition
```bash
mount /dev/sda4 /home
```
That is for the mounting. Now your system is ready to install Arch Linux.