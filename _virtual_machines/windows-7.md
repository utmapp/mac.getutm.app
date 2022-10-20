---
title: Windows 7
architecture: x64
memory: 1 GiB
disk: 20 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: windows-7-x64.png
download: https://github.com/utmapp/vm-downloads/releases/download/windows-template/windows-7-x64-utm.zip
---

## Requirements
You need an Windows 7 installation ISO. There are many different ones that work but a good working image for English users is named `en_windows_7_ultimate_with_sp1_x64_dvd_u_677332.iso` and has the SHA1 hash of `36ae90defbad9d9539e649b193ae573b77a71c83`.

## Installation
1. Open the downloaded template `.utm` and select "Windows 7" UTM.
2. At near the bottom of the screen is "Interface: ide" with an option to select an image.
3. Select your Windows 7 installation ISO.
4. Start the VM.
5. Install Windows 7 with all the default options.
6. After installation, download the [SPICE tools ISO][1].
7. Use the CD icon in the toolbar to eject the Windows installation ISO, and select the SPICE tools ISO.
8. Install the SPICE tools.


[1]: https://docs.getutm.app/guest-support/windows/#download