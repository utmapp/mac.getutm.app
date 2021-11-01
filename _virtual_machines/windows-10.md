---
title: Windows 10/11
architecture: ARM64/x64
memory: 8 GiB
disk: 20 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: windows-10-arm64.png
download: 
---

This guide will help you create an Windows 10 or Windows 11 virtual machine from a fresh install.

## Downloads

* [UTM for Mac](https://github.com/utmapp/UTM/releases)
* [UUP dump](https://uupdump.net)
* [SPICE Guest Tools]({% link support.md %})

## Instructions

These instructions are for those who are already familiar with the UTM interface. If you are a new user, we recommend reading [the Windows 11 ARM64 guide]({% link _virtual_machines/windows-11-arm.md %}) for extra details.

1. Find the edition of Windows you want to install on [UUP dump](https://uupdump.net). Once you downloaded and extracted the installer creator, you need to run `uup_download_macos.sh` to generate the ISO.
2. In UTM, create a new VM for either the x86_64 or ARM64 architecture (under System) depending on the version of Windows you downloaded. Select at least 8 GiB of RAM.
4. Under Drives, create a new drive and check "Removable". On ARM64, it should default to "USB" as the interface and on x86_64, it should default to "IDE".
3. Create another new drive with an amount of storage you need (at least 20 GiB is recommended). On ARM64, make sure to select "NVMe" as the interface. On x86_64, you can leave the default "IDE".
5. Save the VM, and select it in the sidebar. On the bottom right, click Browse and select the Windows ISO you've created in step 1.
6. Start the VM and follow the Windows installer.
7. Once installation is complete, make sure to install the [SPICE Guest Tools]({% link support.md %}) for networking drivers and access to higher resolutions.

## Troubleshooting

### "This PC can't run Windows 11"

If you get this message trying to install Windows 11, you can bypass it with the following steps:

1. Press **Shift+F10** to open Command Prompt and type in `regedit.exe` to launch Registry Editor.
2. Navigate to **HKEY_LOCAL_MACHINE\SYSTEM\Setup**
3. Right click on the **Setup** key on the left size and choose New -> Key.
4. Create a key named `LabConfig`
5. Select the **LabConfig** key.
6. Create two new values: Choose New -> DWORD (32-bit) and create `BypassTPMCheck` and `BypassSecureBootCheck`. Set both values to 1.
7. Close out of Registry Editor and Command Prompt.
8. In setup, press the back button and then Next to continue installation.
