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
* [UUP dump (Windows 10)](https://uupdump.net/known.php?q=21390)
* [UUP dump (Windows 11)](https://uupdump.net/known.php?q=Windows+11+co_release)
* [SPICE Guest Tools]({% link support.md %})

## Instructions

1. Find the edition of Windows you want to install on [UUP dump](https://uupdump.net). Once you downloaded and extracted the installer creator, you need to run `uup_download_macos.sh` from Terminal to generate the ISO. (Read "troubleshooting" below if you are having issues here.)
2. Open UTM and click the "+" button to open the VM creation wizard.
3. Select "Virtualize".
4. Select "Windows".
5. Uncheck "Import VHDX Image" and you should see the text above change to "Boot ISO Image". Press "Browse" and select the ISO you built in step 1.
6. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
7. Specify the maximum amount of drive space to allocate. Press "Next" to continue.
8. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
9. Press "Save" to create the VM and press the Run button to start the VM.
10. Follow the Windows installer. If you have issues with the mouse, press the mouse capture button in the toolbar to send mouse input directly. Press Control+Option together to exit mouse capture mode. Sometimes, due to driver issues, you can enter and exit capture mode and the mouse cursor works normally again.
11. Once installation is complete and you've logged in, we can proceed to install the guest tools. With the ISO mounted in the D: drive, open Windows Explorer and browse to `D:\`. Run `spice-guest-tools-xxx.exe` which should install all drivers along with QEMU agent, SPICE agent (for copy/paste and dynamic resolution), and shared directory.

### Installing the Microsoft Store and UWP apps (optional)

At the time of writing, Microsoft does not provide ARM64 builds of its built-in apps so you must install the x86 version of the Store. To do this, use this [Parallels Desktop guide](https://kb.parallels.com/en/128520#section2) (under "Install Microsoft Store manually") to install the x86 version of the Microsoft Store. Then you can use it to install x86 versions of other built-in apps. You will have to uninstall the ARM32 versions if you installed them through other means.

## Troubleshooting

### Cannot run `uup_download_macos.sh`

First, make sure that `uup_download_macos.sh` is executable by running

```
$ chmod +x uup_download_macos.sh
```

If you are on Apple Silicon, you need to install Homebrew under Rosetta 2

```
$ softwareupdate --install-rosetta
$ arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
$ arch -x86_64 brew tap sidneys/homebrew
$ arch -x86_64 brew install aria2 cabextract wimlib cdrtools sidneys/homebrew/chntpw
```

Then you can run `uup_download_macos.sh`

```
$ ./uup_download_macos.sh
```

### Boots into EFI shell instead of Windows installer

Make sure you generated the right ISO for your architecture. Note that **arm64** is for Apple Silicon and **amd64** is for Intel.

### Installer crashes with BSOD `SYSTEM_THREAD_EXCEPTION_NOT_HANDLED`

You are using a version of Windows that is too old. The build number should be 21390 or higher.

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

### Ping does not work

Note that due to libslirp limitations, `ping` will not work and so Windows may think that there is still no internet connection.

### Networking does not work

Make sure you installed the SPICE guest tools, which includes the network drivers.
