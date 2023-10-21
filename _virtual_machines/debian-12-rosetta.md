---
title: Debian 12 (Rosetta)
architecture: ARM64
memory: 4 GiB
disk: 64 GiB
display: VGA
spice_installed: true
username: debian
password: debian
screenshot: debian-12-arm64.png
guide: https://docs.getutm.app/guides/debian/
download: https://archive.org/download/debian-12-rosetta-arm64-utm/debian-12-rosetta-arm64-utm.zip
utm_link: true
---
An Apple Silicon Mac running macOS 12+ is required. This image has Rosetta pre-configured along with amd64 multiarch support installed. To install x86_64 packages, append `:amd64` to the name. For example:

```
$ sudo apt install hello:amd64
```

Note that Rosetta does not currently support i386 packages so that multiarch is not enabled.
