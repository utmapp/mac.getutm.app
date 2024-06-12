---
title: ArchLinux ARM
architecture: ARM64
memory: 2048 MiB
disk: 10 GiB
display: Console
spice_installed: false
username: root
password: root
screenshot: archlinux-logo.png
download: https://github.com/utmapp/vm-downloads/releases/download/archlinux-arm64/archlinux-arm64-utm4.zip
utm_link: true
---


## Enable clipboard, directory sharing and full screen

from https://wiki.archlinux.org/title/QEMU#SPICE 

install the following:

```
$ sudo pacman -S spice-vdagent xf86-video-qxl
```

With the VM turned off, open the settings, and make sure Enable Clipboard Sharing and Enable Directory Sharing are checked.





