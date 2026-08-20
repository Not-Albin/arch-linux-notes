<div align="center">

[← Home](../README.md) • [Installation](.) • [← Base Install](base-install.md) • [Next: Locale & Timezone →](locale-and-timezone.md)

</div>

---

# Bootloader
> [Arch Wiki: GRUB](https://wiki.archlinux.org/title/GRUB) & [Arch Wiki: systemd-boot](https://wiki.archlinux.org/title/Systemd-boot)

Making your system actually boot. GRUB is what I use.

Inside the chroot, install the right packages for your setup:

**UEFI:**
```bash
pacman -S grub efibootmgr os-prober
```

**BIOS:**
```bash
pacman -S grub
```

Then install to the disk:

**UEFI:**
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

**BIOS:**
```bash
grub-install --target=i386-pc /dev/nvme0n1
```

On BIOS, that goes to the whole disk, not a partition.

**Dual booting:**

Make sure the below mentioned command is uncomment.

```bash
nano /etc/default/grub
uncomment this line:
GRUB_DISABLE_OS_PROBER=false
```
Save it.

Generate the config:
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

If `grub-install` complains about not finding the EFI directory, you did not mount the EFI partition to `/boot` before chrooting. Reboot the ISO, remount, chroot, and try again. I have made this mistake more than once.

## systemd-boot

Minimal alternative for UEFI-only:

```bash
pacman -S efibootmgr
bootctl install
```

Create `/boot/loader/entries/arch.conf`:
```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options root=UUID=YOUR-ROOT-UUID rw
```

Find your UUID with `blkid /dev/nvme0n1p3`.

## Dual Boot with Windows

os-prober should detect Windows when you run `grub-mkconfig`. If not:
- Make sure both Windows and Linux are configured for BIOS or both for UEFI.  Os-prober won't detect if the modes are mismatched.
- Install `fuse3`. This will definitely fix this issue, if not refer arch-wiki.

```bash
sudo pacman -S fuse3
```

No boot entry after install? Some UEFI firmwares are picky. Add it manually:

```bash
efibootmgr --create --disk /dev/nvme0n1 --part 1 --label "Arch Linux" --loader "\EFI\GRUB\grubx64.efi"
```