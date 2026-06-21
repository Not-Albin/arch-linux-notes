# Pre-Install Checklist
> [Arch Wiki: Installation guide](https://wiki.archlinux.org/title/Installation_guide)

Before you touch a single partition, run through this checklist. Trust me, verifying the ISO actually matters — I have seen people install from a corrupted image and wonder why everything breaks.

## Grab the ISO and check it

```bash
curl -O https://mirror.rackspace.com/archlinux/iso/latest/archlinux-x86_64.iso
curl -O https://mirror.rackspace.com/archlinux/iso/latest/archlinux-x86_64.iso.sig
gpg --keyserver-options auto-key-retrieve --verify archlinux-x86_64.iso.sig
```

A `Good signature` line means the ISO is legit. Skipping this is not worth the risk.

## Make the bootable USB

With `dd`:

```bash
lsblk   # Triple-check which device is your USB
sudo dd if=archlinux-x86_64.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

Or just use Ventoy. I use Ventoy because swapping ISOs without re-flashing the stick is easier:

```bash
sudo ./Ventoy2Disk.sh -i /dev/sdX
# Then copy the ISO to the Ventoy partition
```

## Disable Secure Boot

Arch ISOs do not boot with Secure Boot. Disable it in your firmware (UEFI) settings before booting. I have spent more time than I care to admit staring at a black screen because I forgot this.

## Check if you booted UEFI or BIOS

During boot, if the menu shows `UEFI`, you are in UEFI mode. Check from the live ISO too:

```bash
ls /sys/firmware/efi/efivars
```

If the directory exists and has files, you are in UEFI mode. If not, you are in BIOS (legacy) mode.

## Get online

Ethernet: plug it in. Live ISO auto-configures DHCP.

Wi-Fi with `iwctl`:

```bash
iwctl
[iwd]# device list
[iwd]# station wlan0 scan
[iwd]# station wlan0 get-networks
[iwd]# station wlan0 connect YOUR_SSID
```

Verify with `ping -c 3 archlinux.org`.

## Watch out for

- Writing `dd` to a partition instead of the whole device (`/dev/sda1` instead of `/dev/sda`). Ask me how I know.
- Booting the wrong entry on a dual-boot machine. If you see Windows Boot Manager, you picked the wrong USB boot entry. Pick the one labelled `USB: ...` or `UEFI: ...` without the Windows name.
- Forgetting to disable Secure Boot. You will get an untrusted file error and stare at the screen wondering what happened.