---
title: Windows XP
architecture: x64
memory: 512 MiB
disk: 20 GiB
display: VGA
spice_installed: true
username:
password:
screenshot: windows-xp-x64.png
download: https://github.com/utmapp/vm-downloads/releases/download/windows-template/windows-xp-x64-utm.zip
---

## Requirements
You need an Windows XP installation ISO. There are many different ones that work but a good working image for English users is named `en_windows_xp_professional_sp3_Nov_2013_Incl_SATA_Drivers.iso` and has the SHA1 hash of `6947e45f7eb50c873043af4713aa7cd43027efa7`.

## Installation
1. Open the downloaded template `.utm` and select "Windows XP" in UTM.
2. At near the bottom of the screen is "Interface: ide" with an option to select an image.
3. Select your Windows XP installation ISO.
4. Start the VM.
5. Install Windows XP with all the default options.
6. After installation, download the [SPICE tools ISO][1].
7. Use the CD icon in the toolbar to eject the Windows installation ISO, and select the SPICE tools ISO.
8. Install the SPICE tools.

## Notes
Due to the age of this operating system, Internet Explorer 6 will NOT work at loading most websites even if internet is working. You should download [Firefox 52 ESR][2], the last version to support Windows XP and use UTM's directory sharing feature to install it.


[1]: {% link support.md %}
[2]: https://www.mozilla.org/en-US/firefox/52.9.0/system-requirements/
