# Pacman Errors
> [Arch Wiki: Pacman](https://wiki.archlinux.org/title/Pacman)
Recovering from common package management failures. We have all been there.

## 1. Signature Errors
If you see `invalid or corrupted package (PGP signature)`:
```bash
sudo pacman-key --init
sudo pacman-key --populate archlinux
sudo pacman -S archlinux-keyring
```

## 2. Partial Upgrades
Arch does not support partial upgrades. If you manually updated a package and others broke, do a full sync:
```bash
sudo pacman -Syu
```

## 3. Database Lock
If pacman says `unable to lock database`:
```bash
sudo rm /var/lib/pacman/db.lck
```
This happens if a previous pacman installation crashed or was interrupted. I have had to do this after a power cut.

## 4. Failed Mirrorlist
If every package download fails with a 404:
```bash
sudo reflector --country 'India' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
sudo pacman -Syu
```

## Common Mistakes
- **Running `pacman -S` without `-yu` after not updating for weeks.** This causes a partial upgrade state. Always sync before installing.
- **Deleting `/var/lib/pacman/db.lck` while pacman is actually running.** Check `ps aux | grep pacman` first. Do not be that person.
