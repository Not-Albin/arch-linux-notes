<div align="center">

[← Home](../README.md) • [Troubleshooting](.) • [Next: Network Debug →](network-debug.md)

</div>

---

# Common Boot Issues
> [Arch Wiki: Boot loaders](https://wiki.archlinux.org/title/Boot_loaders)
Recovering from a system that will not boot. This section exists because I have broken my bootloader enough times to know the pain.

## Prerequisites
- An Arch live USB.
- Patience.

## 1. Boot from Live USB and Mount Everything
```bash
lsblk
mount /dev/nvme0n1p3 /mnt        # root partition
mount /dev/nvme0n1p1 /mnt/boot    # EFI partition
arch-chroot /mnt
```

## 2. Reinstall GRUB
If GRUB was overwritten or the EFI entry was deleted:
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

## 3. Re-create the EFI Boot Entry
If your UEFI firmware no longer lists Arch:
```bash
efibootmgr --create --disk /dev/nvme0n1 --part 1 --label "Arch Linux" --loader "\EFI\GRUB\grubx64.efi"
```

## 4. The Rescue Shell
If you see a `grub rescue>` prompt, your `grub.cfg` is missing or the partition UUID changed.

From the rescue shell:
```
set prefix=(hd0,gpt3)/boot/grub
set root=(hd0,gpt3)
insmod normal
normal
```

Boot into Arch, then re-run `grub-mkconfig`.


## Dual Boot issues
If os-prober didn't detect window, make sure that:
- Both Windows and Linux is configured for BIOS or UEFI. If one is BIOS and other is UEFI, then os-prober won't detect it.
- Install fuse3, I had the similar issue os-prober not detecting, but after installing fuse3 fixed my issue.
```bash
sudo pacman -S fuse3
```
## Common Mistakes
- **Chrooting without mounting the EFI partition.** If `/boot` is empty inside the chroot, GRUB will install to the wrong place. I have done this.
- **Running `grub-install` to a partition on BIOS systems.** On BIOS, install to the disk (`/dev/nvme0n1`), not a partition.
