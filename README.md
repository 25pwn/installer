# Installer

**This is alpha quality software; things are almost guaranteed to change or fail. Use at your own risk.**

Installs a linux distro in a fully unattended, configurable manner

Currently supports installing archlinux

## Planned
- Signing on `nicopwn` repo
- Dependency system
- Parallel install
- Fedora Rawhide support
- LUKS2 support
- Update daemon

## Requirements
- A working `arch-install-scripts` installation
- `systemd-nspawn`

## Usage
`# installer <action> CONFIGDIR`

actions:
- `install`: installs according to `CONFIGDIR`
- `reinstall`: wipes and installs according to `CONFIGDIR`
- `nshell`: starts a systemd-nspawn shell according to `CONFIGDIR`
- `cshell`: starts a chroot shell according to `CONFIGDIR`

CONFIGDIR:
- `configs/defaults` is a valid and the default `CONFIGDIR`
- `CONFIGDIR/config` contains information about the install
- `CONFIGDIR/scripts` contains the scripts to be executed during the install
- `CONFIGDIR/nspawn` contains the configurations for the systemd-nspawn container
- `configs/defaults/config` is always sourced before `CONFIGDIR/config`
- Even if you specify your own `CONFIGDIR`, only `CONFIGDIR/config` is used by default; set `$configdir` in your `CONFIGDIR/config` to use your whole `CONFIGDIR`

## Notes
- Make sure your drives are partitioned and formatted before starting your install. In particular, the default config specifies a btrfs subvolume to install to; make sure it exists or remove the subvolume-related mount options.
- `initramfs` files are generated inside the container, so make sure you use the fallback `initramfs` before updating them.