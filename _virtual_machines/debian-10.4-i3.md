---
title: Debian 10.4 (Custom i3)
architecture: ARM64
memory: 1024 MiB
disk: 10 GiB
display: VGA+Console
spice_installed: true
username: debian
password: debian
screenshot: debian-10.4-i3-arm64.png
download: https://github.com/utmapp/vm-downloads/releases/download/debian-10.4/debian-10.4-i3-arm64-utm.zip
utm_link: true
---
## Notes
* Root account username/password is `root`/`password`. You should change this.
* Due to a bug auto resolution does not work. Run `xrandr --output Virtual-1 --auto` to resize.
* Custom built from a minimal Linux install
* i3 Window Manager with LightDM for maximum performance
* Customized xterm theme
* Working audio, networking, sharing features
* In VGA mode, /media/share mounts the share directory at startup
* Alias commands `resize` refreshes resolution of the display and `soundon` enables audio
