# Base Install
> [Arch Wiki: Installation guide](https://wiki.archlinux.org/title/Installation_guide)

After partitions are mounted, throw the base system onto the disk.

## Mirrors first
Slow mirrors mean slow install. This saves a lot of waiting around.

```bash
reflector --country 'India' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```
Change 'India' to your country.

## Pacstrap

```bash
pacstrap -K /mnt base base-devel linux linux-firmware linux-headers vim nano git man-db man-pages texinfo intel-ucode
```

The `-K` flag sets up pacman keys inside the new system. I used to forget that.

> **Why so many extras:** `linux-headers` because you'll need them for DKMS later. `intel-ucode` because microcode updates are not optional on Intel — switch to `amd-ucode` if you're on AMD. Read [Arch Wiki: Microcode](https://wiki.archlinux.org/title/Microcode). The rest are just things you will want inside the chroot (editors, git, man pages).


## Make fstab

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
This tells the system to mount all the partition during every boot.

Always check it after:

```bash
cat /mnt/etc/fstab
```

Look for your partitions by UUID. If a partition is missing here, it will not mount on boot.

## Chroot in

```bash
arch-chroot /mnt
```

Prompt changes. You are no longer on the live ISO from this point.

Set the root password before doing anything else:

```bash
passwd
```

## Speed pacman up inside the chroot

```bash
nano /etc/pacman.conf
```

Uncomment:
```
Color
ParallelDownloads = 5
```

Makes a surprising difference when you start pulling down desktop stuff.

## Don't forget
- If you did not mount everything before `pacstrap`, you'll get a silent failure. The ISO's `/mnt` is empty if nothing is mounted there.
- If you start setting hostname and timezone before `arch-chroot`, you're configuring the live ISO, which gets thrown away on reboot.