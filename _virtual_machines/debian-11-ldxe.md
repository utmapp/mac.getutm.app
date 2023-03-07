---
title: Debian 11 (LXDE)
architecture: ARM64
memory: 1024 MiB
disk: 20 GiB
display: VGA+Console
spice_installed: true
username: debian
password: debian
screenshot: debian-11-ldxe-arm64.png
download: https://github.com/utmapp/vm-downloads/releases/download/debian-11.5/debian-11.5-ldxe-arm64-utm4.zip
utm_link: true
---
## Notes
* Root account username/password is `root`/`password`. You should change this.
* Due to a bug auto resolution does not work. Run `xrandr --output Virtual-1 --auto` to resize.