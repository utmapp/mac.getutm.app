---
title: Windows 10/11 (ARM64 versions)
architecture: ARM64
memory: 8 GiB
disk: 20 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: windows-11.png
download: 
---

This guide is designed to only work with Apple Silicon Macs.

## Downloads

* [UTM for Mac](https://github.com/utmapp/UTM/releases)
* [Windows for ARM ISO](https://uup.rg-adguard.net/)
* [SPICE Guest Tools]({% link support.md %})

## Generate a Windows 10/11 ARM64 installer ISO

Note: you do need a recent version of Windows 11 or Windows 10 on x86_64 computer to generate an ISO.

For Windows 11 ARM 64 installer ISO:
1. On the Windows for ARM ISO page, select following
2. Select type: `Cumulative Update for Windws 10`
3. Select version: `\[22000.651] 2022-04 Cumulative Update for Windows 11 for arm64-based Systems (KB5012643) \[arm64]` or another Windows 11 `arm64` build (but not an Insider nor preview build)

For Windows 10 ARM 64 installer ISO (method 1):
1. On the Windows for ARM ISO page, select following
2. Select type: `Windows (Final version)`
3. Select version: `Feature update to Windows 10, version 21H2 \[arm64]` or another Windows 10 `arm64` build

For Windows 10 ARM 64 installer ISO (method 2, if method 1 does not work):
1. On the Windows for ARM ISO page, select following
2. Select type: `Cumulative Update for Windws 10`
3. Select version: `\[19044.1469] 2022-01 Cumulative Update for Windows 10 Version 21H2 for arm64-based Systems (KB5010793) \[arm64]` or another Windows 10 `arm64` build (but not an Insider nor preview build)

The rest of steps remain same
4. Select language: `en-us: English (United States)` or a language of your choice
5. Select edition: `All Edition`
6. Select type download: `Download ISO compiler in OneClick! (run downloaded CMD-file)`
7. On the right-hand column, make sure you download the `.cmd` file starting with `multi_creatingISO...` 
8. This script allows you to remove hardware installation restriction for Windows 11. To reduce the time generating ISO file, recommend to turn off `Integrate Cumulative Updates` in the `.cmd` script.
9. Finally, you will have ISO generated, and you can use it in UTM to install Windows 10/11

## Instructions

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Windows".
4. Click "Browse" and select the Windows ISO downloaded above. Press "Next" to continue.
5. Pick the amount of RAM and CPU cores you wish to give access to the VM. Press "Next" to continue.
6. If you have a directory you want to mount in the VM, you can select it here. Alternatively, you can skip this and select the directory later from the VM window's toolbar. The shared directory will be available after installing SPICE tools (see below). Press "Next" to continue.
7. Press "Save" to create the VM and press the Run button to start the VM.
8. Follow the Windows installer. If you have issues with the mouse, press the mouse capture button in the toolbar to send mouse input directly. Press Control+Option together to exit mouse capture mode. Sometimes, due to driver issues, you can enter and exit capture mode and the mouse cursor works normally again.
9. Once installation is complete and you've logged in, we can proceed to install the guest tools. With the ISO mounted in the D: drive, open Windows Explorer and browse to `D:\`. Run `spice-guest-tools-xxx.exe` which should install all drivers along with QEMU agent, SPICE agent (for copy/paste and dynamic resolution), and shared directory.

### Installing the Microsoft Store and UWP apps (optional)

At the time of writing, Microsoft does not provide ARM64 builds of its built-in apps so you must install the x86 version of the Store. To do this, use this [Parallels Desktop guide](https://kb.parallels.com/en/128520#section2) (under "Install Microsoft Store manually") to install the x86 version of the Microsoft Store. Then you can use it to install x86 versions of other built-in apps. You will have to uninstall the ARM32 versions if you installed them through other means.

## Troubleshooting

### Ping does not work

Note that due to libslirp limitations, `ping` will not work and so Windows may think that there is still no internet connection.

### Networking does not work

Make sure you installed the SPICE guest tools, which includes the network drivers.

If Windows 11 setup is stuck due to lack of network connection:

1. Press **Shift + F10** to launch Command Prompt.
2. Type in `OOBE\BYPASSNRO` and press Enter.
3. Your VM should reboot and at the setup screen you should see an option for "I don't have internet."
4. Once Windows setup is completed, make sure to install the SPICE guest tools for network drivers.
