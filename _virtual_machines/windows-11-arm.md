---
title: Windows 11
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
* [Windows for ARM](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64)
* [SPICE Guest Tools]({% link support.md %})

## Instructions

1. Open UTM and click the "+" button to open the VM creation wizard.
2. Select "Virtualize".
3. Select "Windows".
4. Click "Browse" and select the Windows VHDX downloaded above. Press "Next" to continue.
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
