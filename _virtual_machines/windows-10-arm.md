---
title: Windows 10
architecture: ARM64
memory: 8 GiB
disk: 20 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: windows-10-arm64.png
download: 
---

This guide is designed to only work with Apple Silicon Macs.

## Downloads

* [UTM for Mac](https://github.com/utmapp/UTM/releases) (v2.0.15 or higher)
* [Windows for ARM](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64) (build 20231 or higher)
* [SPICE Guest Tools]({% link support.md %}) (v0.164 or higher)

## Instructions

{:start="1"}
1. Open UTM and create a new virtual machine.

![Step 1](/images/guides/windows_screen_1.png)

{:start="2"}
2. Give the VM a name and optionally choose an icon.

![Step 2](/images/guides/windows_screen_2.png)

{:start="3"}
3. In System, select the "ARM64 (aarch64)" architecture, and specify the amount of memory. At least half of your computer's total memory is recommended for performance.

![Step 3](/images/guides/windows_screen_3.png)

{:start="4"}
4. In Drives, select "Import Drive" and select the Windows 10 VHDX that you've downloaded. (Please read the troubleshooting section below about a bug with VHDX in QEMU.)

![Step 4](/images/guides/windows_screen_4.png)

{:start="5"}
5. After importing the drive, you must set the interface to NVMe.

![Step 5](/images/guides/windows_screen_5.png)

{:start="6"}
6. Now click "New Drive" and check Removable and click Create to make add CD drive.

![Step 6](/images/guides/windows_screen_6.png)

{:start="7"}
7. Save the VM, and select it in the sidebar. On the bottom right, click Browse and select the SPICE guest tools ISO.

![Step 7](/images/guides/windows_screen_7.png)

{:start="8"}
8. Follow the Windows installer. If you have issues with the mouse, press the mouse capture button in the toolbar to send mouse input directly. Press Control+Option together to exit mouse capture mode. Sometimes, due to driver issues, you can enter and exit capture mode and the mouse cursor works normally again.

![Step 8](/images/guides/windows_screen_8.png)

{:start="9"}
9. Once installation is complete and you've logged in, we can proceed to install the guest tools. With the ISO mounted in the D: drive, open Windows Explorer and browse to `D:\`. Run `spice-guest-tools-xxx.exe` which should install all drivers along with QEMU agent, SPICE agent (for copy/paste and dynamic resolution), and shared directory.

![Step 9](/images/guides/windows_screen_9.png)

Note that due to libslirp limitations, `ping` will not work and so Windows may think that there is still no internet connection.

### Enable Higher Resolutions

{:start="10"}
10. After installing the SPICE guest tools, go to the desktop, right click anywhere, and choose Display Settings.

![Step 10](/images/guides/windows_screen_10.png)

{:start="11"}
11. Scroll down to "Multiple displays" and select "Show only on 1". The mouse might be stuck in the second display so you will have to use the keyboard to confirm and then restart.

![Step 11](/images/guides/windows_screen_11.png)

### Share files with host

{:start="12"}
12. With the VM shut down, open the settings and go to the Sharing tab. Make sure "Enable directory sharing" is checked.

![Step 12](/images/guides/windows_screen_12.png)

{:start="13"}
13. Under "Shared Directory" click Browse and select the directory to share with the VM.

![Step 13](/images/guides/windows_screen_13.png)

Once booted, with the SPICE guest tools installed, the shared directory should show up as a Network Drive.

## Troubleshooting

### System drive gets corrupted

Due to an issue with QEMU handling of VHDX images, sometimes Windows will be corrupted from normal usage. This would result in BSOD or random application crashes/errors. To work around this issue, it is recommended that you convert the VHDX image to a QCOW2 image. Currently, UTM does not provide this functionality in the UI so you have to do it directly from QEMU.

1. Install [Homebrew](https://brew.sh) if you do not have it already.
2. Run `brew install qemu`
3. Run `qemu-img convert -p -O qcow2 /path/to/Windows10_InsiderPreview_Client_ARM64_en-us_21286.VHDX /path/to/output/Windows10_InsiderPreview_Client_ARM64_en-us_21286.qcow2` replacing the paths with your own.
4. Use the QCOW2 image with UTM. It is recommended you do this with a fresh VHDX from Microsoft in case your image was already corrupted.
