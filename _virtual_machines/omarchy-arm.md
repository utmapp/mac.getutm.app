---
title: Omarchy 4 ARM64
architecture: ARM64
memory: 4 GiB
disk: 80 GiB
display: GPU Accelerated
spice_installed: true
username: omarchy
password: omarchy
screenshot: omarchy-arm64.png
guide: https://github.com/ggalancs/omarchy-arm-utm
download: https://archive.org/details/omarchy-arm-utm
utm_link: false
---
Arch Linux ARM with the [Omarchy 4](https://omarchy.org) desktop: Hyprland
0.56.2, quickshell as bar, menu, OSD and notification daemon, hyprlock,
hypridle, uwsm and SDDM with autologin, plus the 456 `omarchy-*` commands.

Omarchy has no aarch64 build — its package repository serves x86_64 only — so
this rebuilds the desktop on Arch Linux ARM and applies the real contents of the
Omarchy tree. The 18 packages that upstream does not publish for ARM are compiled
from source — nine of them Omarchy's own, `herdr` included — and OBS Studio and
Pinta are included.

The image ships a neutral `us` keyboard layout, with Option acting as SUPER so
Omarchy's shortcuts are reachable from a Mac keyboard. The timezone is UTC;
set yours with `sudo timedatectl set-timezone <zone>`.

The VM is configured with the GPU-capable display device
(`virtio-gpu-gl-pci`), but the desktop renders in software by default, because
under UTM 4.7 GPU clients come up black. Two reports on UTM 5.0.x describe that
bug as gone; `omarchy-arm-gpu --on` switches to hardware GL there, and `--off`
goes back. `omarchy-arm-display --retina` moves the desktop to 3840x2400 at
scale 2 for a sharp panel, and `--default` goes back. `omarchy-arm-user`
switches which account logs in automatically.

It is configured for 4 GiB and 4 vCPU. That is not a minimum: booted read-only,
the desktop comes up clean on 1536 MiB, and at 1024 the OOM killer takes
quickshell. Lower it in the VM settings if your Mac is tight.

Shared clipboard works in both directions with "Share clipboard" enabled and the
VM open as a window. Shared folders work in both VirtFS and SPICE WebDAV modes:
pick one in the VM settings and run `omarchy-arm-share` in the guest.

With software rendering, blur and shadows are off; turning the GPU on brings
them back. The resolution is fixed at boot and editable in
`~/.config/hypr/monitors.lua`.

Change the password with `passwd` as soon as you log in. The build script that
produces this image is at
[ggalancs/omarchy-arm-utm](https://github.com/ggalancs/omarchy-arm-utm).
