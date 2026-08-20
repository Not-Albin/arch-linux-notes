<div align="center">

[← Home](../README.md) • [Installation](.) • [← Bootloader](bootloader.md)

</div>

---

# Locale and Timezone
> [Arch Wiki: Locale](https://wiki.archlinux.org/title/Locale) & [Arch Wiki: Time](https://wiki.archlinux.org/title/Time)

The boring but necessary part. Do this inside the chroot.

## Timezone

List zones:
```bash
ls /usr/share/zoneinfo/Asia/
```

Link yours:
```bash
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
```

Replace `Asia/Kolkata` with your city. Sync the hardware clock after:

```bash
hwclock --systohc
```

## Locale

Edit `/etc/locale.gen` and uncomment your language line:

```bash
nano /etc/locale.gen
```

For UK English:
```
en_GB.UTF-8 UTF-8
```
For English (India):
```
en_IN.UTF-8 UTF-8
```
For US English:
```
en_US.UTF-8 UTF-8
```

Generate it:
```bash
locale-gen
```

Create `/etc/locale.conf`:
```bash
echo "LANG=en_GB.UTF-8" > /etc/locale.conf
```

Forgetting to run `locale-gen` after editing `locale.gen` is a common mistake. Applications will complain about missing locale settings.

## Hostname

```bash
echo "archie" > /etc/hostname
```

Edit `/etc/hosts`:
```
127.0.0.1   localhost
::1         localhost
127.0.1.1   archie
```

Replace `archie` with whatever hostname you picked.

If you dual-boot with Windows and the clock is constantly wrong, read [Arch Wiki: Time](https://wiki.archlinux.org/title/Time). Windows and Linux fight over DST settings.
