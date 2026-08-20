<div align="center">

[← Home](../README.md) • [Post-Install](.) • [Next: Networking →](networking.md)

</div>

---

# Users and Sudo
> [Arch Wiki: Users and groups](https://wiki.archlinux.org/title/Users_and_groups) & [Arch Wiki: Sudo](https://wiki.archlinux.org/title/Sudo)
Creating an unprivileged user for daily use and giving them root access via `sudo`. Do not skip this.

## Why Not Root?
Running as root all the time is dangerous. A typo or a compromised script can nuke your entire system. Arch is do-it-yourself, so the safety rails are thinner than on other distros. Use a normal user and escalate only when needed. 

## Create a User
```bash
useradd -m -G wheel -s /bin/bash albin
```
- `-m` creates a home directory at `/home/albin`.
- `-G wheel` adds the user to the `wheel` group, the conventional group for sudoers.
- `-s /bin/bash` sets the default shell.

Set a password:
```bash
passwd albin
```

## Install and Configure Sudo
```bash
pacman -S sudo
```

Allow members of the `wheel` group to use `sudo` by editing the sudoers file:
```bash
EDITOR=vim visudo
```

Uncomment this line:
```
%wheel ALL=(ALL:ALL) ALL
```

Save and exit. Now the `albin` user can run root commands with `sudo`.

## Test It
Exit the chroot (or open a new terminal), log in as your new user, and try:
```bash
sudo whoami
```
It should return `root`. If it does not, something went wrong with the sudoers file.

## Common Mistakes
- **Creating a user without a home directory.** If you forget `-m`, the user has no home folder and many applications will complain.
- **Forgetting to set a password.** A user with no password cannot log in or use `sudo`.
- **Editing `/etc/sudoers` directly with a normal text editor.** Always use `visudo`; it checks syntax before saving. I once broke sudo this way and had to boot from a live ISO to fix it.
