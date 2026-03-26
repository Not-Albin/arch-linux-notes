# Arch Linux Notes
A practical documentation of my Arch Linux setup. From the base installation to daily use. 

This is not a copy-paste guide. 
It's a collection of what I actually used, what I have broke, and how I fixed it.


## Who this is for?

- Beginners trying Arch for first time.
- People tired of vague tutorials.
- Beginner friendly Arch-wikii guides(Not all, only the important ones)

---

## :wrench: What this repo covers?
- Manual Arch Linux installation.
- Bootloader setup
- Basic System configuration
- i3 window manager setup
- Common mistakes and fixes
---

## :notebook: Installation Overview
These are some basic steps I followed:
```bash
# Partition disk
# Format partitions
# Mount filesystem

pacstrap /mnt base linux linux-firmware

genfstab -U /mnt >> /mnt/etc/fstab

arch-chroot /mnt
```
After that: 
- Set timezone, locale and hostname
- Install bootloader(GRUB)
- Create a user and passwords

Full detailed steps are inside the /installation folder.

## :memo: Configuration
After installation:
- Installed and configured i3 window manager(you can use a desktop environment like KDE plasma)
- Enabled NetworkManager for Wi-Fi
- Tweaked system for daily usability

 Check /configuration for details.
