# Partitioning
> [Arch Wiki: Partitioning](https://wiki.archlinux.org/title/Partitioning)

Creating space for Arch on your disk.

```bash
lsblk
```

Find your actual drive. `loop0` is the live ISO, `sda` might be a USB stick, and `nvme0n1` (or `sda` if it is not removable) is probably your internal drive. Look for the largest non-removable disk.

## UEFI (GPT) Layout

| Mount Point | Type          | Size           |
|-------------|---------------|----------------|
| `/boot`     | EFI System    | 300 MiB        |
| `[SWAP]`    | Linux swap    | Equal to RAM   |
| `/`         | Linux x86-64  | 20 GiB+        |
| `/home`     | Linux x86-64  | Rest of disk   |

`/home` is optional, if you prefer to separate your personal files from `/root`,then it's better to use a separate `/home` partitioning.

With `cfdisk`:

```bash
cfdisk /dev/nvme0n1   # Replace with your disk
```

1. Create a `New` partition of `300M`, set `Type` to `EFI System`.
2. Create `New` swap (e.g., `8G`), set `Type` to `Linux swap`.
3. Create `New` root (e.g., `50G`), set `Type` to `Linux filesystem`.
4. Create `New` home with the remaining space.
5. `Write` the table, then `Quit`.

## BIOS (MBR) Layout

Same as above but:
- Disk label must be `dos` (MBR)
- Root partition (`/`) must be set as `Bootable`
- `/boot` is just `Linux`, not `EFI System`

## Formatting

```bash
# EFI
mkfs.fat -F 32 /dev/nvme0n1p1

# Root and home
mkfs.ext4 /dev/nvme0n1p3
mkfs.ext4 /dev/nvme0n1p4
```

## Swap

If you made a swap partition:

```bash
mkswap /dev/nvme0n1p2
swapon /dev/nvme0n1p2
```

I prefer a swapfile instead — more flexible. Skip the swap partition during partitioning, then after base install inside the chroot:

```bash
dd if=/dev/zero of=/swapfile bs=1M count=8192 status=progress
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

Add to `/etc/fstab`:
```
/swapfile none swap defaults 0 0
```

## Mount everything

```bash
mount /dev/nvme0n1p3 /mnt
mkdir -p /mnt/boot
mount /dev/nvme0n1p1 /mnt/boot
mkdir /mnt/home
mount /dev/nvme0n1p4 /mnt/home
swapon /dev/nvme0n1p2
```

Check with `lsblk` that everything is mounted where you expect.

If you skip `/mnt/boot`, GRUB will fail later with no EFI partition found. I have been there.
