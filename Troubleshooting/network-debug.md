<div align="center">

[← Home](../README.md) • [Troubleshooting](.) • [← Boot Issues](common-boot-issues.md) • [Next: Black Screen After Login →](black-screen-after-login.md)

</div>

---

# Network Troubleshooting
> [Arch Wiki: Network configuration](https://wiki.archlinux.org/title/Network_configuration) & [Arch Wiki: Wireless network configuration](https://wiki.archlinux.org/title/Wireless_network_configuration)
Diagnosing Wi-Fi and wired connection problems. Usually it is something dumb that I forgot to check.

## 1. Is the Interface Up?
```bash
ip link
```
Look for `state UP`. If it is `DOWN`:
```bash
sudo ip link set wlan0 up
```

## 2. Check rfkill
```bash
rfkill list
```
If it says `Soft blocked: yes`:
```bash
rfkill unblock wifi
```

## 3. Missing Firmware
If `dmesg | grep -i firmware` shows missing files, install the firmware package for your chipset:
```bash
sudo pacman -S linux-firmware
```

For Realtek USB adapters (e.g., `rtl8821cu`):
```bash
yay -S rtl8821cu-dkms
```
If the built-in kernel driver isn't working, make sure to download and install dkms driver of your respectively USB adapter. Use the AUR package, it is easiler than manually installing dkms driver. 

## 4. Ethernet Not Working
Check the cable and the link lights. Then:
```bash
dhcpcd eth0
```

If `dhcpcd` is not installed:
```bash
sudo pacman -S dhcpcd
```

## Common Mistakes
- **Assuming Wi-Fi works out of the box.** Some chipsets need proprietary firmware that is not in `linux-firmware`. Check `dmesg` first.
- **Forgetting to enable the NetworkManager service after installing it.** `sudo systemctl enable --now NetworkManager`. Yes, this is a mistake I have made.
