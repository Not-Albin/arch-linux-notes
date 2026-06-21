# Picom
> [Arch Wiki: Picom](https://wiki.archlinux.org/title/Picom)
Adding transparency, shadows, and smooth window transitions. Also fixes screen tearing on some setups.

## Prerequisites
- A working Xorg session (i3, Openbox, etc.).

## 1. Install Picom
```bash
sudo pacman -S picom
```

## 2. Basic Configuration
Create `~/.config/picom/picom.conf`:
```
backend = "glx"
vsync = true

shadow = true
shadow-radius = 7
shadow-opacity = 0.75
shadow-offset-x = -7
shadow-offset-y = -7

fading = true
fade-in-step = 0.03
fade-out-step = 0.03
```

## 3. Autostart
Add to your i3 config or `.xinitrc`:
```
picom --config ~/.config/picom/picom.conf &
```

Or simply:
```
picom &
```
if the defaults are fine for you.

## 4. Fix Screen Tearing
If you see tearing, try the experimental backends:
```
backend = "glx"
swap-method = "buffer-age"
```

## Common Mistakes
- **Running picom without a configuration file and getting broken transparency.** Some applications (like terminals) need explicit opacity rules if you want them semi-transparent.
- **Forcing `vsync = true` on a buggy driver.** If picom causes stutter, disable vsync and rely on the driver's own vsync. I had to do this on an old Intel laptop.
