<div align="center">

[← Home](../README.md) • [Post-Install](.) • [← AUR Helpers](aur-helpers.md)

</div>

---

# Pacman Basics
> [Arch Wiki: Pacman](https://wiki.archlinux.org/title/Pacman)
The single most important tool on your system. Learn these commands and you will be fine.

## Essential Commands

Sync package database and upgrade all packages:
```bash
sudo pacman -Syu
```

Install a package:
```bash
sudo pacman -S firefox
```

Remove a package:
```bash
sudo pacman -R firefox
```

Remove a package and its orphaned dependencies:
```bash
sudo pacman -Rs firefox
```

Search for a package:
```bash
pacman -Ss firefox
```

Query installed packages:
```bash
pacman -Q firefox
```

List all explicitly installed packages:
```bash
pacman -Qe
```

Clean package cache (keeps only the latest version):
```bash
sudo pacman -Sc
```

## Tweaking `/etc/pacman.conf`
Open `/etc/pacman.conf` and ensure these lines are uncommented for a better experience:
```
Color
ParallelDownloads = 5
```

Enable the `multilib` repository for 32-bit compatibility (needed for Steam and some Wine games):
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

## Update Mirrors with Reflector
```bash
sudo pacman -S reflector
sudo reflector --country 'India' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

## Common Mistakes
- **Running `pacman -Syu` while in a graphical session without checking for breaking changes.** Always read the Arch news (https://archlinux.org/news/) before updating. Major library updates can break your desktop. I learned this the hard way when a KDE update broke my session.
- **Partial upgrades.** Never run `pacman -S` package without `-yu` first. Partial state is unsupported and frequently breaks.
- **Forgetting to update the mirrorlist periodically.** Mirrors go stale; using a fast, updated mirror makes a huge difference.
