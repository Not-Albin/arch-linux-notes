<div align="center">

# Arch Linux Notes

Personal notes from installing and running Arch as a daily driver.  
What worked, what broke, and how I fixed it.

[Installation](#installation) • [Post-Install](#post-install) • [Desktop](#desktop) • [Troubleshooting](#troubleshooting)

</div>

---

## What this is

A collection of short, practical guides covering the path from Arch ISO to a usable desktop. These are **my** notes — not a replacement for the [Arch Wiki](https://wiki.archlinux.org). Use them as a faster reference when you already know the basics or just need the exact commands and gotchas I hit.

**Suggested order for a fresh install:**
1. Installation (in order)
2. Post-Install
3. Desktop (if you want a graphical environment)
4. Troubleshooting (keep this bookmarked)

---

## Installation

| Guide | What it covers |
|-------|----------------|
| [Pre-Install Checklist](Installation/pre-install-checklist.md) | ISO verification, bootable USB, UEFI vs BIOS, getting online |
| [Partitioning](Installation/partitioning.md) | Disk layouts for UEFI/BIOS, swap, formatting, mounting |
| [Base Install](Installation/base-install.md) | Pacstrap, fstab, arch-chroot, essential packages |
| [Bootloader](Installation/bootloader.md) | GRUB (UEFI/BIOS), systemd-boot, dual-boot Windows |
| [Locale & Timezone](Installation/locale-and-timezone.md) | Language, time, hostname, hosts file |

---

## Post-Install

| Guide | What it covers |
|-------|----------------|
| [Users & Sudo](Post-Install/users-and-sudo.md) | Create user, wheel group, sudo config |
| [Networking](Post-Install/networking.md) | NetworkManager, Wi-Fi, static IP, DNS |
| [Audio](Post-Install/audio.md) | PipeWire, testing, troubleshooting |
| [AUR Helpers](Post-Install/aur-helpers.md) | yay/paru, what the AUR is, safety |
| [Pacman Basics](Post-Install/pacman-basics.md) | Core commands, pacman.conf tweaks, mirrors |

---

## Desktop

| Guide | What it covers |
|-------|----------------|
| [i3 Window Manager](Desktop/i3wm-setup.md) | i3, dmenu/rofi, wallpaper, autostart |
| [Display Manager](Desktop/display-manager.md) | LightDM, greetd, autologin |
| [Fonts & Theming](Desktop/fonts-and-theming.md) | Nerd Fonts, GTK themes, cursors, icons |
| [Picom](Desktop/picom.md) | Compositor, vsync, transparency, tearing fixes |

---

## Troubleshooting

| Guide | What it covers |
|-------|----------------|
| [Boot Issues](Troubleshooting/common-boot-issues.md) | GRUB rescue, missing EFI entry, chroot recovery |
| [Network Debug](Troubleshooting/network-debug.md) | Wi-Fi issues, missing firmware, rfkill, rtl8821cu |
| [Black Screen After Login](Troubleshooting/black-screen-after-login.md) | Xorg not starting, missing drivers, .xinitrc |
| [Pacman Errors](Troubleshooting/pacman-errors.md) | Signatures, partial upgrades, database locks, mirrors |

---

## One rule

> [!IMPORTANT]
> **Read [Arch News](https://archlinux.org/news/) before every `pacman -Syu`.**  
> Updating after a long gap without checking the news is the fastest way to break your system. I’ve done it more than once.

The [Arch Wiki](https://wiki.archlinux.org) remains the real reference. These notes are just a shortcut.

---

*Last updated: August 2026*