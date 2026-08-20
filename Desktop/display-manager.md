<div align="center">

[← Home](../README.md) • [Desktop](.) • [← i3 Window Manager](i3wm-setup.md) • [Next: Fonts & Theming →](fonts-and-theming.md)

</div>

---

# Display Manager
> [Arch Wiki: Display manager](https://wiki.archlinux.org/title/Display_manager)
Adding a graphical login screen so you do not need to type `startx` every time. I used to just use `startx` but a display manager is more convenient.

## Prerequisites
- A desktop environment or window manager is installed.

## LightDM (What I use with pals)
Install LightDM and the GTK greeter:
```bash
sudo pacman -S lightdm lightdm-gtk-greeter
```

Enable the service:
```bash
sudo systemctl enable lightdm
```

Configure the greeter in `/etc/lightdm/lightdm.conf`:
```
[Seat:*]
greeter-session=lightdm-gtk-greeter
user-session=i3
```

## Greetd (Minimal Alternative)
`greetd` is a lightweight display manager that pairs well with `tuigreet` for a terminal-style login:
```bash
sudo pacman -S greetd tuigreet
```

Enable:
```bash
sudo systemctl enable greetd
```

Edit `/etc/greetd/config.toml`:
```
[terminal]
vt = 1

[default_session]
command = "tuigreet --cmd i3"
user = "greeter"
```

## Autologin (Optional)
In `/etc/lightdm/lightdm.conf`:
```
[Seat:*]
autologin-user=albin
autologin-session=i3
```

## Common Mistakes
- **Enabling both LightDM and Greetd.** Only one display manager can run at a time. Pick one and disable the other.
- **Setting the wrong `user-session`.** If LightDM boots to a black screen, check that the session name matches the `.desktop` file in `/usr/share/xsessions/`. I spent half an hour on this once.
