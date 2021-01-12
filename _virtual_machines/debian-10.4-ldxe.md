---
title: Debian 10.4 (LDXE)
architecture: ARM64
memory: 1024 MiB
disk: 10 GiB
display: VGA+Console
spice_installed: true
username: debian
password: debian
screenshot: debian-10.4-ldxe-arm64.png
download: https://github.com/utmapp/vm-downloads/releases/download/debian-10.4/debian-10.4-ldxe-arm64-utm.zip
---
## Notes
* Root account username/password is `root`/`password`. You should change this.
* Due to a bug auto resolution does not work. Run `xrandr --output Virtual-1 --auto` to resize.