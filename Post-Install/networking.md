# Networking
> [Arch Wiki: Network configuration](https://wiki.archlinux.org/title/Network_configuration) & [Arch Wiki: NetworkManager](https://wiki.archlinux.org/title/NetworkManager)
Getting online. NetworkManager is what I use on all my Arch installs because it just works.

## Prerequisites
You have rebooted into your new Arch system or are still in the chroot.

## 1. NetworkManager (What I recommend)
Install NetworkManager and the command-line tools:
```bash
pacman -S networkmanager network-manager-applet
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
```

### Wi-Fi with nmcli
List devices:
```bash
nmcli device status
```

Scan and connect:
```bash
nmcli device wifi list
nmcli device wifi connect "SSID" password "password"
```

### Interactive TUI
```bash
nmtui
```
I actually prefer `nmtui` when I am too lazy to remember the exact `nmcli` incantation.

## 2. iwd backend (Faster, lightweight)
NetworkManager can use `iwd` instead of `wpa_supplicant`:
```bash
sudo pacman -S iwd
```

Edit `/etc/NetworkManager/NetworkManager.conf`:
```
[device]
wifi.backend=iwd
```

Restart NetworkManager:
```bash
sudo systemctl restart NetworkManager
```

## 3. Static IP
If you need a fixed IP (e.g., for a server), use `nmcli`:
```bash
nmcli con add type ethernet con-name "wired-static" ifname eth0 ip4 192.168.1.10/24 gw4 192.168.1.1
nmcli con mod "wired-static" ipv4.dns "1.1.1.1,8.8.8.8"
nmcli con up "wired-static"
```

## 4. DNS
NetworkManager usually handles DNS automatically. To use a specific DNS server globally, edit `/etc/resolv.conf` or configure it via NetworkManager:
```bash
nmcli con mod "Your Connection" ipv4.dns "1.1.1.1"
```

## Common Mistakes
- **Forgetting to `enable` NetworkManager.** If you only install it but do not enable the systemd service, networking will not start on boot. I have made this mistake at least twice.
- **Conflicting with systemd-networkd.** If you enabled both, they will fight. Pick one. NetworkManager is the safer default for desktops.
