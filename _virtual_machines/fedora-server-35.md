---
title: Fedora Server 35
architecture: ARM64
memory: 4 GiB
disk: 2 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: fedora-server-35-arm64.png
download:
---

This guide is designed to only work with Apple Silicon Macs.

## Downloads

* [UTM for Mac](https://github.com/utmapp/UTM/releases) (v3.0 or higher)
* [Fedora 35 Standard ISO image for aarch64 ISO](https://getfedora.org/en/server/download/)

## Creating a new virtual machine

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Linux".
4. Click "Browse" and select the Fedora Server Live ISO downloaded from the link above. (e.g., "Fedora-Server-dvd-aarch64-35-1.2.iso") Press "Next" to continue.
5. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
6. Specify the maximum amount of drive space to allocate. Press "Next" to continue.
7. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
8. Press "Save" to create the VM and press the Run button to start the VM.
9. Go through the Fedora installer. Click "Install to Hard Drive", select Language, under "Sytem", click "Installation Destination". Click "Disk image", then "Done" in top left corner. Under "User Settings", click "root", add password and click "Done". Click "Begin Installation". When it is done, click "Reboot". Power down the VM.
10. Edit the VM you just created, but right clicking on the name and "Edit". Select "USB Drive", then "move down". (so the disk image will boot first")

## Enable clipboard and directory sharing

Install the following:

```
$ sudo dnf install spice-vdagent spice-webdavd
```

