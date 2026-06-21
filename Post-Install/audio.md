# Audio
> [Arch Wiki: PipeWire](https://wiki.archlinux.org/title/PipeWire)
Getting sound working. PipeWire is the modern replacement for PulseAudio and it is what I use.

## Prerequisites
You are logged into your new Arch system.

## 1. Install PipeWire
```bash
sudo pacman -S pipewire pipewire-pulse pipewire-alsa wireplumber
```

> **Beginner note:** PipeWire is the audio server. `wireplumber` is the session manager that decides which microphone and speakers to use. `pipewire-pulse` provides compatibility with applications that expect PulseAudio. I once tried running PipeWire without `wireplumber` and had zero sound until I realised the session manager was missing.

## 2. Enable the Services
```bash
systemctl --user enable pipewire
systemctl --user enable wireplumber
systemctl --user start pipewire
systemctl --user start wireplumber
```

## 3. Verify Audio
List sinks (outputs):
```bash
wpctl status
```

Test with `pactl`:
```bash
pactl info
```

Play a test sound:
```bash
speaker-test -c 2
```

Set the default sink:
```bash
wpctl set-default SINK_ID
```
Replace `SINK_ID` with the number from `wpctl status`.

## Common Mistakes
- **Installing both PipeWire and PulseAudio.** They will conflict. Only install `pipewire-pulse` (which provides PulseAudio compatibility) and not the standalone `pulseaudio` package.
- **Forgetting to start the user services.** PipeWire runs per-user, not system-wide. Use `systemctl --user`, not `sudo systemctl`.
