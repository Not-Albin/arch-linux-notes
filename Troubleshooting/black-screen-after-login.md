# Black Screen After Login
> [Arch Wiki: Xorg](https://wiki.archlinux.org/title/Xorg)
Fixing the situation where you log in and see only a black screen. Or get dumped back to the login prompt.

## 1. Check if Xorg Starts Manually
Switch to a TTY (Ctrl+Alt+F3), log in, and try:
```bash
startx
```

If it fails, read the error:
```bash
cat /var/log/Xorg.0.log | grep -i error
```

## 2. Missing `.xinitrc`
If you are not using a display manager, create `~/.xinitrc`:
```bash
#!/bin/sh
exec i3
```

Make it executable:
```bash
chmod +x ~/.xinitrc
```
I forgot this step once and wondered why `startx` did nothing.

## 3. Missing Video Drivers
Install the appropriate driver:
```bash
# Intel
sudo pacman -S xf86-video-intel

# AMD
sudo pacman -S xf86-video-amdgpu

# NVIDIA (open)
sudo pacman -S xf86-video-nouveau
```

## 4. Permissions
Ensure your user is in the `video` group:
```bash
sudo usermod -aG video $USER
```

Log out and back in for group changes to take effect.

## Common Mistakes
- **Running `startx` as root.** Xorg should be started by your normal user. I made this mistake when I was new to Linux.
- **Installing proprietary NVIDIA drivers without following the Arch Wiki steps.** The proprietary NVIDIA driver requires extra configuration. Read [Arch Wiki: NVIDIA](https://wiki.archlinux.org/title/NVIDIA) carefully.
