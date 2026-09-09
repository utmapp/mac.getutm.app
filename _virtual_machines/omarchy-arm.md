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

Arch Linux ARM with the [Omarchy 4](https://omarchy.org) desktop: Hyprland 0.56.2,
quickshell as bar, menu and notifications, hyprlock, hypridle, uwsm, and SDDM with
autologin. Omarchy publishes no aarch64 build, so this is rebuilt on Arch Linux ARM;
the build script is linked above.

## Notes
* Username/password is `omarchy`/`omarchy`. Change it with `passwd` on first login.
* The keyboard is `us`, with Option (⌥) as SUPER so Omarchy's shortcuts are reachable from a Mac keyboard. The timezone is UTC.
* Rendering is software by default, so blur and shadows are off. `omarchy-arm-gpu --on` switches to hardware GL where the host supports it, `--off` goes back.
* The resolution is 1920x1200, fixed at boot. `omarchy-arm-display --retina` moves it to 3840x2400 at scale 2, `--default` returns.
* Shared clipboard works both ways with "Share clipboard" enabled. For shared folders, choose VirtFS or SPICE WebDAV in the VM settings and run `omarchy-arm-share` in the guest.
* Configured for 4 GiB and 4 vCPU, which is not a minimum: the desktop comes up on 1536 MiB, and at 1024 the OOM killer takes quickshell.
