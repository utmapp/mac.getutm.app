---
title: Omarchy 4 ARM64
architecture: ARM64
memory: 12 GiB
disk: 80 GiB
display: VGA
spice_installed: true
username: omarchy
password: omarchy
screenshot: omarchy-arm64.png
guide: https://github.com/ggalancs/omarchy-arm-utm
download: https://archive.org/details/omarchy-arm-utm
utm_link: false
---
Arch Linux ARM with the [Omarchy 4](https://omarchy.org) desktop: Hyprland
0.56.1, quickshell as bar, menu, OSD and notification daemon, hyprlock,
hypridle, uwsm and SDDM with autologin, plus the 445 `omarchy-*` commands.

Omarchy has no aarch64 build — its package repository serves x86_64 only — so
this rebuilds the desktop on Arch Linux ARM and applies the real contents of the
Omarchy tree. The 18 packages that upstream does not publish for ARM are compiled
from source — nine of them Omarchy's own, `herdr` included — and OBS Studio and
Pinta are included.

The image ships a neutral `us` keyboard layout, with Option acting as SUPER so
Omarchy's shortcuts are reachable from a Mac keyboard.

Rendering is software by default, because under UTM 4.7 GPU clients come up
black. On UTM 5.0.x that is not the case: `omarchy-arm-gpu --on` switches to
hardware GL, and `--off` goes back. `omarchy-arm-user` switches which account
logs in automatically.

Shared clipboard works in both directions with "Share clipboard" enabled and the
VM open as a window. Shared folders work in both VirtFS and SPICE WebDAV modes:
pick one in the VM settings and run `omarchy-arm-share` in the guest.

With software rendering, blur and shadows are off; turning the GPU on brings
them back. The resolution is fixed at boot and editable in
`~/.config/hypr/monitors.lua`.

Change the password with `passwd` as soon as you log in. The build script that
produces this image is at
[ggalancs/omarchy-arm-utm](https://github.com/ggalancs/omarchy-arm-utm).
