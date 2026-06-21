# i3 Window Manager Setup
> [Arch Wiki: i3](https://wiki.archlinux.org/title/I3)
Installing and configuring a tiling window manager. i3 is my go-to because it stays out of the way.

## Prerequisites
- Xorg is installed (`xorg-server`, `xorg-xinit`).
- You can start X with `startx`.

## 1. Install i3 and Dependencies
```bash
sudo pacman -S i3-wm i3status dmenu rofi xterm
```

> **Beginner note:** A window manager controls where windows appear. A desktop environment (like KDE) includes a file manager, browser, and more. i3 is just a window manager, so you build the rest yourself. I like this; others hate it.

## 2. Initial Configuration
On first launch, i3 asks you to create a config file. Press `Enter` to create one at `~/.config/i3/config`.

Key bindings to learn immediately:
| Key | Action |
|-----|--------|
| `Mod+Enter` | Open a terminal |
| `Mod+d` | Open dmenu (application launcher) |
| `Mod+Shift+q` | Close focused window |
| `Mod+Shift+e` | Exit i3 |
| `Mod+Shift+r` | Restart i3 (reloads config) |

> **Beginner note:** The `Mod` key is usually `Alt` (Mod1) or the Windows key (Mod4). I set mine to the Windows key because it is closer to my thumb.

## 3. Set the Mod Key
Edit `~/.config/i3/config`:
```
set $mod Mod4
```

## 4. Wallpaper
Install `feh` or `nitrogen`:
```bash
sudo pacman -S feh
```

Add to your i3 config:
```
exec --no-startup-id feh --bg-scale /path/to/wallpaper.jpg
```

## 5. Autostart Applications
In `~/.config/i3/config`:
```
exec --no-startup-id nm-applet
exec --no-startup-id picom
```

## Common Mistakes
- **Forgetting to install a terminal emulator.** i3 does not include one. `xterm` is a safe default, but most people switch to `alacritty` or `kitty`. I use `alacritty`.
- **Editing the config while i3 is running and wondering why changes do not apply.** Restart i3 with `Mod+Shift+r` after saving. I still forget this sometimes.
