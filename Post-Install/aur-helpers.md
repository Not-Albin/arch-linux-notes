# AUR Helpers
> [Arch Wiki: Arch User Repository](https://wiki.archlinux.org/title/Arch_User_Repository)
Automating AUR package builds so you do not have to manually run `makepkg` every time.

> **Warning about compromised AUR packages:** Recently, several AUR packages have been uploaded backdoored with malware. Outdated dependencies or abandoned packages can become attack vectors. Never install anything from the AUR without reading the upstream URL and the `PKGBUILD` first. If something looks off, skip it.

## What Is the AUR?
The AUR is a community-driven repository of package build scripts (`PKGBUILDs`). Unlike official packages, AUR packages are not pre-built or officially vetted. I always skim the `PKGBUILD` before building, especially for packages with low popularity or few votes. It is a good habit.

## Install `yay`

```bash
sudo pacman -S --needed git base-devel
```

```bash
git clone https://aur.archlinux.org/yay.git
```

```bash
cd yay
makepkg -si
```

## Using `yay`
Search and install:
```bash
yay -S spotify
```

Update everything (official + AUR):
```bash
yay -Syu
```

Remove build dependencies after install:
```bash
yay -Sc
```

## `paru` (Alternative)
`paru` is a newer helper written in Rust with very similar commands:
```bash
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

Usage is almost identical:
```bash
paru -S spotify
paru -Syu
```

## When to Be Careful
- Packages with few votes or recent maintainer changes.
- Packages that download pre-built binaries instead of building from source (check the `source=()` line in the `PKGBUILD`).
- Any package asking for your sudo password with a suspicious `PKGBUILD`.


## Common Mistakes
- **Blindly installing AUR packages without reading the `PKGBUILD`.** Malicious or abandoned packages can and do exist. I always check the upstream URL at minimum.
- **Running `makepkg` as root.** Always build as a normal user. `makepkg` will refuse to run as root anyway.
