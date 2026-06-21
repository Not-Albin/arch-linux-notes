# Arch Linux Notes

My notes on getting Arch Linux running. From the first boot of the ISO to a fully configured daily driver.

This is not a copy-paste guide. It is stuff I have actually used, stuff I have broken, and how I fixed it.

## Who This Is For

- **Complete beginners** who want a clear path through the Arch install without the noise of outdated tutorials.
- **Regular Arch users** who need a quick reference for common tasks — setting up a new desktop, debugging a black screen, fixing pacman, whatever.

---

## Table of Contents

### Installation
- [Pre-Install Checklist](Installation/pre-install-checklist.md) — ISO verification, bootable USB, UEFI vs BIOS, getting online.
- [Partitioning](Installation/partitioning.md) — Disk layouts for UEFI and BIOS, swap options, formatting and mounting.
- [Base Install](Installation/base-install.md) — Pacstrap, fstab, arch-chroot, and essential packages.
- [Bootloader](Installation/bootloader.md) — GRUB for UEFI and BIOS, systemd-boot, dual boot with Windows.
- [Locale and Timezone](Installation/locale-and-timezone.md) — Language, time, hostname, and hosts file.

### Post-Install
- [Users and Sudo](Post-Install/users-and-sudo.md) — Creating a user, wheel group, sudo configuration.
- [Networking](Post-Install/networking.md) — NetworkManager, Wi-Fi, static IP, DNS.
- [Audio](Post-Install/audio.md) — PipeWire setup, testing, and troubleshooting.
- [AUR Helpers](Post-Install/aur-helpers.md) — What the AUR is, yay and paru, safety tips.
- [Pacman Basics](Post-Install/pacman-basics.md) — Essential commands, pacman.conf tweaks, mirror management.

### Desktop
- [i3 Window Manager Setup](Desktop/i3wm-setup.md) — i3, dmenu/rofi, wallpaper, autostart.
- [Display Manager](Desktop/display-manager.md) — LightDM, greetd, autologin.
- [Fonts and Theming](Desktop/fonts-and-theming.md) — Nerd Fonts, GTK themes, cursor and icon packs.
- [Picom](Desktop/picom.md) — Compositor setup, vsync, transparency, fixing screen tearing.

### Troubleshooting
- [Common Boot Issues](Troubleshooting/common-boot-issues.md) — GRUB rescue, missing EFI entry, chroot recovery.
- [Network Debug](Troubleshooting/network-debug.md) — Wi-Fi issues, missing firmware, rfkill, rtl8821cu.
- [Black Screen After Login](Troubleshooting/black-screen-after-login.md) — Xorg not starting, missing drivers, .xinitrc.
- [Pacman Errors](Troubleshooting/pacman-errors.md) — Signatures, partial upgrades, database locks, broken mirrors.

---

## A Note on Maintenance

Arch is a rolling-release distribution. Before updating, always check the [Arch News](https://archlinux.org/news/) for manual interventions. Running `sudo pacman -Syu` blindly after a long gap can break things. I have learned this the hard way more than once.

If something goes wrong, the [Arch Wiki](https://wiki.archlinux.org) remains the definitive source of truth. This repository is a companion, not a replacement.
