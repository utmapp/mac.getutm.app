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
download: https://github.com/utmapp/vm-downloads/releases/download/archlinux-arm64/archlinux-arm64-utm.zip
utm_link: true
---


## Enable clipboard and directory sharing

from https://wiki.archlinux.org/title/QEMU#SPICE 

```
$ sudo pacman -S spice-vdagent xf86-video-qxl
```

With the VM turned off, open the settings, and make sure these two options are checked.

![Sharing](/images/guides//ubuntu_screen_sharing.png)




