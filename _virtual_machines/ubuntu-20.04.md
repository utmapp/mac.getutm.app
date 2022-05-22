---
title: Ubuntu 20.04
architecture: ARM64
memory: 8 GiB
disk: 10 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: ubuntu-20.04-arm64.png
download: 
---

This guide is designed to only work with Apple Silicon Macs.

## Downloads

* [UTM for Mac](https://github.com/utmapp/UTM/releases) (v3.0 or higher)
* [Ubuntu Server for ARM](https://ubuntu.com/download/server/arm) (20.04.1 or higher)

## Creating a new virtual machine

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Linux".
4. Click "Browse" and select the Ubuntu Server ISO downloaded from the link above. Press "Next" to continue.
5. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
6. Specify the maximum amount of drive space to allocate. Press "Next" to continue.
6. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
8. Press "Save" to create the VM and press the Run button to start the VM.
9. Go through the Ubuntu Server installer. If the reboot fails, you can manually quit the VM, unmount the installer ISO, and start the VM again to boot into your new installation.

## Use Geo-optimized mirrors

The default `ports.ubuntu.com` repository mirror is a bit slow and only use http (which is insecure), hence we recommend installing Ubuntu without network connection first until we configure it to use a secure HTTPS mirror.

You can use an alternative mirror by visiting this site [Official Archive Mirrors for Ubuntu](https://launchpad.net/ubuntu/+archivemirrors), search for Ports, and use an HTTPS mirror.

For instance, United States users can use [Open Computing Facility at UC Berkeley (Ports)](https://mirrors.ocf.berkeley.edu/ubuntu-ports/), you can use this command line

```

$ sudo sed -E -i 's#http://[^\s]*ports\.ubuntu\.com/ubuntu-ports/#https://mirrors.ocf.berkeley.edu/ubuntu-ports/#g' /etc/apt/sources.list'

```

## Installing Ubuntu Desktop

At the end of the installation, you will have Ubuntu Server installed without any GUI. To install Ubuntu Desktop, log in and run:

```
$ sudo apt update
$ sudo apt install ubuntu-desktop
$ sudo reboot
```

## Let Network Manager handle network connection (highly recommend if you install Ubuntu Desktop)

When switching between display modes or changing hardware settings, the network adapter may be renamed by Ubuntu. Fortunately, Network Manager can handle such change, and once you complete these steps, you can actually manage network setting via desktop GUI's native Setting App

In the terminal, go to `/etc/netplan` to see the folder content, it should contain `00-installer-config.yaml`
```
$ cd /etc/netplan
$ ls -l

```

Disable all YAML files by changing `.yaml` to `.yaml.disabled`, such as 

```
$ sudo mv 00-installer-config.yaml 00-installer-config.yaml.disabled

```

Then, create a 01-network-manager-all.yaml by using 

```
$ sudo nano 01-network-manager-all.yaml

```

with the content of 

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager

```

Use Control-X to exit `nano`, and type `y` to commit change.

Finally, let's activate Network Manager Service and disable systemd network service by executing following.

```
$ sudo systemctl disable systemd-networkd
$ sudo systemctl disable networkd-dispatcher.service

$ sudo systemctl enable NetworkManager
$ sudo reboot

```

This has been tested on Ubuntu 22.04

## Enable clipboard and directory sharing

Install the following:

```
$ sudo apt install spice-vdagent spice-webdavd
```

Your shared directory shows up as a WebDAV server on `http://127.0.0.1:9843/`. You can use a WebDAV client to access it, or `mount.davfs` to mount it.


## Troubleshooting

### Cannot boot into installer

If you start the VM and are stuck at the EFI screen (`BdsDxe: failed to load Boot0001` or `UEFI Interactive Shell`), try the following in order.

1. Make sure you have the installer ISO selected. Click the disk icon on the toolbar and check that there is a menu option for `CD/DVD (ISO) Image (usb): ubuntu-xxx.iso`. If it says `CD/DVD (ISO) Image (usb): none`, then highlight that menu and choose `Change` and then select the ISO. If you don't have any selectable menu option, follow the guide again and make sure you have added a removable drive. Then restart the VM.
2. Next, try to get into the EFI Shell. If you see `UEFI Interactive Shell` then you are already in the shell. Otherwise, restart the VM and quickly press the Esc key to enter the shell.
3. In the EFI shell make sure you see `FS0: Alias(s):CD0h0a0a::BLK1:` near the top or something similar. If not, then double check your configuration and make sure you have a removable drive configured and the installer ISO mounted. Also check that your ISO is valid.
4. Type in: `fs0:\efi\boot\bootaa64.efi` and you should see GRUB. Then select `Ubuntu Server` to continue with the install.

### Networking is unavailable (DEPRECATED)

When switching between display modes or changing hardware settings, the network adapter may be renamed by Ubuntu. To fix this, you need to set up networking again.

1. Run `ip link show` and look at the last adapter name. For example, it may be listed as `enp0s9`.
2. Edit `/etc/netplan/00-installer-config.yaml` and copy your configuration for `enp0s8` (or whatever the old adapter was named) and paste it immediately after for `enp0s9` (or whatever the new adapter is named).
3. Reboot and you should be able to use networking in both display modes.

On older versions of Ubuntu and other Linux distributions, you may not have Netplan. In that case, refer to support documents for your distribution on how to set up a new network adapter as the name of the adapter may have changed.
