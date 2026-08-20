<div align="center">

[← Home](../README.md) • [Desktop](.) • [← Display Manager](display-manager.md) • [Next: Picom →](picom.md)

</div>

---

# Fonts and Theming
> [Arch Wiki: Fonts](https://wiki.archlinux.org/title/Fonts)
Making your desktop readable and not ugly. These are the fonts and themes I actually use.

## Prerequisites
- You have a working Xorg or Wayland session.

## 1. Nerd Fonts
Nerd Fonts patch popular fonts with thousands of icons. `ttf-meslo-nerd` is my go-to:
```bash
sudo pacman -S ttf-meslo-nerd ttf-dejavu ttf-liberation
```

Set the default in `~/.config/fontconfig/fonts.conf` or via your terminal emulator's preferences.

## 2. GTK Theming
Install a theme engine and a theme:
```bash
sudo pacman -S gnome-themes-extra arc-gtk-theme
```

To set the theme without a full desktop environment, use `xsettingsd`:
```bash
sudo pacman -S xsettingsd
```

Create `~/.config/xsettingsd/xsettingsd.conf`:
```
Net/ThemeName "Arc-Dark"
Net/IconThemeName "Adwaita"
```

Add to your i3 autostart:
```
exec --no-startup-id xsettingsd
```

## 3. Cursor and Icon Themes
```bash
sudo pacman -S adwaita-icon-theme breeze-icons
```

Set cursor theme in `~/.Xresources`:
```
Xcursor.theme: Breeze_Snow
```

Apply:
```bash
xrdb -merge ~/.Xresources
```

## Common Mistakes
- **Installing Nerd Fonts but not selecting them in your terminal.** The font must be set in your terminal emulator, not just installed. I spent a while wondering why icons were broken before realising this.
- **Expecting GTK apps to look right without `xsettingsd`.** Without it, GTK applications fall back to an ugly default theme.
