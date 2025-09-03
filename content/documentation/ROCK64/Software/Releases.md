---
title: "Releases"
draft: false
menu:
  docs:
    title:
    parent: "ROCK64/Software"
    identifier: "ROCK64/Software/Releases"
    weight: 1
aliases:
  - /wiki/ROCK64_Software_Release
  - /wiki/ROCK64_Software_Releases
---

This page contains a list of all available releases for the [ROCK64](/documentation/ROCK64), as well as links to other resources.

## Linux

### AOSC

{{< figure src="/documentation/images/aosc.png" width="100" >}}

*AOSC OS* is a general purpose Linux distribution that strives to simplify user experience and improve free and open source software for day-to-day productivity. To learn more about AOSC, please visit the official [AOSC website](https://aosc.io/).

Download:

* https://aosc.io/downloads/ (supports the microSD card and eMMC, 8GB or more)

| Default credentials | |
| -------- | ------- |
| `aosc` | `anthon` |

### Arch Linux ARM

{{< figure src="/documentation/images/Archlinux-logo.png" width="100" >}}
Official *Arch Linux ARM* release.

Installation:

* https://archlinuxarm.org/platforms/armv8/rockchip/rock64

### Armbian

{{< figure src="/documentation/images/armbian.png" width="100" >}}

*Armbian* is a Linux distribution designed for ARM boards. They are usually Debian or Ubuntu flavored.

Download:

* [ROCK64's Armbian site](https://www.armbian.com/rock64/) (supports the microSD card and eMMC, 8GB or more)
* [Download archive](https://armbian.tnahosting.net/archive/rock64/archive/) (supports the microSD card and eMMC, 8GB or more)

### ayufan's Linux releases

{{< figure src="/documentation/images/penguin.png" width="100" >}}

The community member _ayufan_ offers multiple ROCK64 Linux releases based on Debian and Ubuntu. The forum thread for release can be found [here](https://forum.pine64.org/showthread.php?tid=6309).

Download:

* https://github.com/ayufan-rock64/linux-build/releases (supports the microSD card and eMMC)

{{< admonition type="note" >}}
 Make sure to download images for the _ROCK64_.
{{</ admonition >}}

| Default credentials | |
| -------- | ------- |
| `rock64` | `rock64` |

### Debian

{{< figure src="/documentation/images/Debian-logo.png" width="100" >}}

*Debian* is an operating system and a distribution of Free Software.

Download:

* [Debian 11 Bullseye](https://deb.debian.org/debian/dists/bullseye/main/installer-arm64/current/images/netboot/SD-card-images/) (recommended)
* [Debian 12 Bookworm](https://deb.debian.org/debian/dists/bookworm/main/installer-arm64/current/images/netboot/SD-card-images/)
* [Daily netboot images](https://d-i.debian.org/daily-images/arm64/)

Instructions:

* Go to the download directory
* Download firmware.rock64-rk3328.img.gz and partition.img.gz
* Combine the 2 parts into 1 image file: `zcat firmware.rock64-rk3328.img.gz partition.img.gz > debian-installer.img`
* Write the created .img file to microSD card or eMMC Module using _dd_: `dd if=debian-installer.img of=/dev/sda bs=4M`. Replace `/dev/sda` with your target drive.
* Plug the microSD/eMMC card in the Rock64 (and connect a serial console) and boot up to start the Debian Installer

Notes:

* An Ethernet connection is required for the above installer
* Remember to leave some space before your first partition for u-boot! You can do this by creating a 32M size unused partition at the start of the device.
* Auto creating all partitions does not work. You can use the following manual partition scheme:

```
#1 - 34MB  Unused/Free Space
#2 - 512MB ext2 /boot           (Remember to set the bootable flag)
#3 - xxGB  ext4 /               (This can be as large as you want. You can also create separate partitions for /home /var /tmp)
#4 - 1GB   swap                 (May not be a good idea if using an SD card)
```

* See [README.concatenateable_images here](https://d-i.debian.org/daily-images/arm64/daily/netboot/SD-card-images/README.concatenateable_images) or [README.concatenateable_images here](https://deb.debian.org/debian/dists/bullseye/main/installer-arm64/current/images/netboot/SD-card-images/README.concatenateable_images) for details regarding the concatenateable images and their installation from non-Linux systems.

### Debian by mrfixit2001

{{< figure src="/documentation/images/Debian-logo.png" width="100" >}}

Mrfixit2001's minimal *Debian* build. Version 190514 onward support Rock64-v3 board

Download:

* [Direct download from mrfixit2001's github](https://github.com/mrfixit2001/debian_builds/releases) (supports the microSD card and eMMC)

| Default credentials | |
| -------- | ------- |
| `rock` | `rock` |

### DietPi

{{< figure src="/documentation/images/dietpi.png" width="100" >}}

*DietPi* is a lightweight yet easy to setup and feature-rich Linux distribution, based on Debian. To find out more about DietPi, please visit the [official documentation](https://dietpi.com/docs/). Discuss the ROCK64 build on the [PINE64 forum thread](https://forum.pine64.org/showthread.php?tid=12514).

Download:

* [Debian 11 Bullseye](https://dietpi.com/downloads/images/DietPi_ROCK64-ARMv8-Bullseye.img.xz) (supports the microSD card and eMMC, 4GB or more)
* [Debian 12 Bookworm](https://dietpi.com/downloads/images/DietPi_ROCK64-ARMv8-Bookworm.img.xz) (supports the microSD card and eMMC, 4GB or more)

| Default credentials | |
| -------- | ------- |
| `root` | `dietpi` |

### Lakka

{{< figure src="/documentation/images/lakka.png" width="100" >}}

*Lakka* is a lightweight Linux distribution that transforms a small computer into a full blown retrogaming console. Visit [PINE64 forum](https://forum.pine64.org/showthread.php?tid=5354) for more information about the Lakka release.

Download:

* https://le.builds.lakka.tv/RK3328.aarch64/ (supports the microSD card and eMMC)

### LibreELEC

{{< figure src="/documentation/images/libreelec.jpg" width="100" >}}

*LibreELEC* is a "Just enough OS" Linux distribution combining the Kodi media center with an operating system.

Download:

* [Official build image](https://libreelec.tv/downloads/rockchip/) (supports the microSD card and eMMC, 8GB or more)
* [Daily builds](https://test.libreelec.tv/) (supports the microSD card and eMMC, 8GB or more)

### Manjaro ARM

{{< figure src="/documentation/images/Manjaro-logo.svg" width="100" >}}

*Manjaro* is a user-friendly Linux distribution based on the independently developed Arch operating system. Manjaro editions for Rock64 are available directly from Manjaro. To learn more about Manjaro please visit the [Manjaro Forum](https://forum.manjaro.org/tags/manjaroarm).

{{< admonition type="note" >}}
 Only supports ROCK64 version 2 SBC!
{{</ admonition >}}

Download:

* [Manjaro ARM ROCK64 GitHub](https://github.com/manjaro-arm/rock64-images/releases) (supports the microSD card and eMMC)

### NEMS Linux

{{< figure src="/documentation/images/nems.jpg" width="100" >}}

*NEMS* stands for "Nagios Enterprise Monitoring Server" and it is a modern pre-configured, customized and ready-to-deploy Nagios Core image designed to run on low-cost micro computers. To find out more on NEMS Linux, please visit their [site](https://nemslinux.com/).

{{< admonition type="warning" >}}
 Only supports ROCK64 ver2 SBC
{{</ admonition >}}

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Download torrent seed from NEMS Linux](https://nemslinux.com/download/nagios-for-pine64.php) (supports the microSD card, 16GB or more, MD5 of the xz file is _6e2088922c5d197db8b8ba3057120389_)
* [Direct download from pine64.org](https://files.pine64.org/os/ROCK64/nems/NEMS_v1.5-Rock64-Build2.zip) (supports the microSD card, 16GB or more, MD5 of the xz file is _6e2088922c5d197db8b8ba3057120389_)

{{< admonition type="note" >}}
 The installation guide can be found [here](https://docs.nemslinux.com/installation).
{{</ admonition >}}

| Default credentials | |
| -------- | ------- |
| `nemsadmin` | `nemsadmin` |

### NextCloudPi

{{< figure src="/documentation/images/nextcloudpi.png" width="100" >}}

*NextCloudPi* comes not only with NextCloud preinstalled, but also with management tools for backups, SSL certificates, SAMBA, enhanced security and more. Visit the project's [website](https://nextcloudpi.com). You can follow the ongoing discussion about NextCloudPi on the [PINE64 forum](https://forum.pine64.org/showthread.php?tid=6047).

Download:

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

* [Direct download from pine64.org](https://files.pine64.org/os/ROCK64/nextcloudplus/NextCloudPi_Rock64_08-01-19.img.gz)

{{< admonition type="note" >}}
 The MD5 hash of the .gz file is _2d3eb799e99a3bb90d5aa7731baf27c6_
{{</ admonition >}}

| Default credentials | |
| -------- | ------- |
| `root` | `1234` |

### OpenMediaVault

{{< figure src="/documentation/images/omv.png" width="100" >}}

*Openmediavault* is the next generation network attached storage (NAS) solution. The forum thread concerning this release can be found [here](https://forum.pine64.org/showthread.php?tid=6309).

Download:

* [Releases on ayufan's github](https://github.com/ayufan-rock64/linux-build/releases/)
* [Direct download from pine64.org (32 bit armhf)](https://files.pine64.org/os/ROCK64/omv/jessie-openmediavault-rock64-0.5.15-136-armhf_sd2emmc.img.xz)
* [Direct download from pine64.org (64 bit arm64)](https://files.pine64.org/os/ROCK64/omv/stretch-openmediavault-rock64-0.9.14-1159-arm64.img.xz)
	
{{< admonition type="note" >}}
 The MD5 hash of the .xz file is _474c2a5aac8874fd188404c8e04e53e8_
{{</ admonition >}}
	
* [Direct download from pine64.org (32 bit armhf)](https://files.pine64.org/os/ROCK64/omv/stretch-openmediavault-rock64-0.9.14-1159-armhf.img.xz)
	
{{< admonition type="note" >}}
 The MD5 hash of the .xz file is _bf5d2ea2bc7a5623ba958ed358a80c2a_
{{</ admonition >}}

| TTY and SSH, except OMV | |
| -------- | ------- |
| `root` | `root` |

| OMV for Web | |
| -------- | ------- |
| `admin` | `openmediavault` |

| OMV for TTY | |
| -------- | ------- |
| `root` | `openmediavault` |

### Recalbox

{{< figure src="/documentation/images/RB.png" width="100" >}}

*Recalbox* is a free and open-source operating system created for the emulation and preservation for retro games. Recalbox allows you to re-play a variety of videogame consoles and platforms in your living room with ease. To find out more about Recalbox and available tweaks to the installation please visit the [PINE64 forum thread](https://forum.pine64.org/showthread.php?tid=7111). Visit the project's [website](https://www.recalbox.com/) for more details.

{{< admonition type="note" >}}
 Only supports ROCK64 ver2 SBC
{{</ admonition >}}

Download:

* [Direct download latest release build from mrfixit2001 GitHub](https://github.com/mrfixit2001/recalbox_rock64/releases) (supports the microSD card and eMMC, 8GB or more)

### R-Cade

{{< figure src="/documentation/images/RCadeLogo.jpg" width="100" >}}

Retro Center's *R-Cade*, the 4K Media Center Arcade. [RCade](https://www.retro-center.com/about-r-cade/) Features 100+ retro-gaming systems, a lightweight web browser, and full 4K UHD media playback.

Download:

* [Direct download from Retro Center's GitHub](https://github.com/retro-center/rcade_releases/releases) (supports the microSD card, eMMC and USB boot)

### Slackware

{{< figure src="/documentation/images/slackware.jpg" width="100" >}}

*Slackware* is a very old, interesting, convenient and easy distribution. Visit the project's website here (https://fail.pp.ua). You can follow the ongoing discussion about Slackware on the PINE64 forum (https://forum.pine64.org/showthread.php?tid=5868)

{{< admonition type="note" >}}
 This Slackware build using the ZST compression algorithm, please visit the [ZST GitHub site](https://github.com/facebook/zstd) for a decompression utility.
{{</ admonition >}}

Download:

* http://dl.fail.pp.ua/slackware/images/rock64/ (supports the microSD card)

| Default credentials | |
| -------- | ------- |
| `root` | `password` |

Flashing the distribution to the eMMC:

* Flash the image to micro SD, power up the board with micro SD and login
* Copy the image file to micro SD by using SFTP. The image file must have the _.img_ file extension.
* After finish copy the file, power off the board and add eMMC module to the board
* Boot the board, run below command for flashing to eMMC module
* Run `sudo dd if=[IMAGE] of=/dev/[DEVICE] bs=10M` (example: _sudo dd if=slack-current-aarch64-xfce_08May18-4.4.126-rock64-build-20180508.img of=/dev/mmcblk1 bs=10M_).
* then edit these two files in eMMC module:
  * `mount /dev/mmcblk1p1 /media`
  * `echo "rootdev=/dev/mmcblk1p1" >> /media/boot/uEnv.txt`
  * `sed -i 's:mmcblk0p1:mmcblk1p1:' /media/etc/fstab`
* After that, power off the board and remove the microSD card. Then boot with only the eMMC module.

## BSD

### FreeBSD

{{< figure src="/documentation/images/Freebsd_Logo.png" width="100" >}}

*FreeBSD* is an operating system used to power modern servers, desktops, and embedded platforms. The [RockChip FreeBSD page](https://wiki.freebsd.org/arm/RockChip#Rock64) has instructions for installing FreeBSD. Version 13.0 and greater include prebuilt images.

Download:

* Images for various FreeBSD releases can be found [here](https://www.freebsd.org/where/)

| SSH access (enabled by default) | |
| -------- | ------- |
| `freebsd` | `freebsd` |

| Root user | |
| -------- | ------- |
| `root` | `root` |

### NetBSD

{{< figure src="/documentation/images/netbsd.png" width="100" >}}

*NetBSD* is a free, fast, secure, and highly portable Unix-like Open Source operating system. To learn more about NetBSD please visit [NetBSD main page](https://www.netbsd.org/).

Download:

* [Direct download](https://armbsd.org/) (select _ROCK64_, supports the microSD card and eMMC)

Notes:

* Instructions concerning enabling SSH can be found [here](https://www.netbsd.org/docs/guide/en/chap-boot.html#chap-boot-ssh) or the bootable image from armbsd.org can have the MSDOS partition modified to setup SSH using [this](https://man.netbsd.org/creds_msdos.8) method.

| Default credentials | |
| -------- | ------- |
| `root` (root and SSH) | none |

### OpenBSD

{{< figure src="/documentation/images/Puffy_mascot_openbsd.png" width="100" >}}

*OpenBSD* is a security-focused, free and open-source, Unix-like operating system based on the Berkeley Software Distribution. You can install OpenBSD on your Rock64 by following [these instructions](https://github.com/krjdev/rock64_openbsd).

## Android

{{< figure src="/documentation/images/Android_logo_2019_(stacked).svg" width="100" >}}

### Android TV 9.x eMMC (No Google Play)

The *Android 9.0* image for eMMC boot. For the installation of the Playstore on Android 9.0 please follow [this forum thread](https://forum.pine64.org/showthread.php?tid=8655).

Image downloads (for direct flashing):

* Stock images (write the image to eMMC module using an USB adapter for the eMMC module)
  * [Stock image for the 16GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190617_stock_android_9.0_emmcboot-16GB.img.gz) from _pine64.org_ (560MB, MD5 of the Gzip file _D985808B4CA912201372DC2F5F322AE9_, build 20190617)
  * [Stock image for the 32GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190617_stock_android_9.0_emmcboot-32GB.img.gz) from _pine64.org_ (579MB, MD5 of the Gzip file _5D65A44F78BD08B4584413C8BEEAAF05_, build 20190617)
  * [Stock image for the 64GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190617_stock_android_9.0_emmcboot-64GB.img.gz) from _pine64.org_ (615MB, MD5 of the Gzip file _B34D1C119386CBA1658E5F0FB9E4413D_, build 20190617)

* Rooted images (write the image to eMMC module using an USB adapter for the eMMC module)
  * [Rooted image for 16GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190618_stock_rooted_android_9.0_emmcboot-16GB.img.gz) from _pine64.org_ (561MB, MD5 of the Gzip file _DBB5B3D46B77A33BC9F09173C9788E6E_, build 20190618)
  * [Rooted image for 32GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190618_stock_rooted_android_9.0_emmcboot-32GB.img.gz) from _pine64.org_ (579MB, MD5 of the Gzip file _5F3B97EA72B3227082500B3FB1FAB44A_, build 20190618)
  * [Rooted image for 64GB eMMC module](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190618_stock_rooted_android_9.0_emmcboot-64GB.img.gz) from _pine64.org_ (615MB, MD5 of the Gzip file _6833B124ABA3AC2269A6B4F51EFD1109_, build 20190618)

Image downloads (for Rockchip Tool):

* [Stock image](https://files.pine64.org/os/ROCK64/android/ROCK64_20190617_stock_android_9.0_emmcboot.img.gz) from _pine64.org_ (544MB, MD5 of the Gzip file _9B717263E7749A732C8B5C7D7D59C5C6_, build 20190617)
* [Rooted image](https://files.pine64.org/os/ROCK64/android/ROCK64_20190618_stock_rooted_android_9.0_emmcboot.img.gz) from _pine64.org_ (544MB, MD5 of the Gzip file _FC5F80C3A939AD0F8DCE5B85F22D20A1_, build 20190618)

{{< admonition type="note" >}}
 See the guide to flashing eMMC using Rockchip Tools. Please unzip the file first and then use Rockchip tool to flash it. The OTG port located at top USB 2.0 port and it needs USB type A to type A cable.
{{</ admonition >}}

Notes:

* Please allow 10-15 minutes on first boot for initialization

### Android 9.x (No Google Play)

The rooted *Android 9.0 TV* image for booting from the microSD card. For the installation of the Playstore on Android 9.0 please follow [this forum thread](https://forum.pine64.org/showthread.php?tid=8655).

Image downloads (for direct flashing):

* [Image for 8GB microSD cards](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190621_stock_rooted_android_9.0_sdboot-8GB.img.gz) from _pine64.org_ (546MB, MD5 of the Gzip file _A250B72CD6AAB24B8156DE08EB15530C_, build 20190621)
* [Image for 16GB microSD cards](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190621_stock_rooted_android_9.0_sdboot-16GB.img.gz) from _pine64.org_ (556MB, MD5 of the Gzip file _09A6BACD71159853D5E4C6C21C883B0F_, build 20190621)
* [Image for 32GB microSD cards](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190621_stock_rooted_android_9.0_sdboot-32GB.img.gz) from _pine64.org_ (574MB, MD5 of the Gzip file _C68DC5D96F1C546B96EC690CE7BFE910_, build 20190621)
* [Image for 64GB microSD cards](https://files.pine64.org/os/ROCK64/android/ROCK64_dd_20190621_stock_rooted_android_9.0_sdboot-64GB.img.gz) from _pine64.org_ (707MB, MD5 of the Gzip file _4EFC87B4CEE4C7655618DCA95EF7DD0D_, build 20190621)

{{< admonition type="note" >}}
 Flash the file to the microSD card, for example using _dd_.
{{</ admonition >}}

Image downloads (for Rockchip SDDisk Tool):

* [Direct download](https://files.pine64.org/os/ROCK64/android/ROCK64_20190621_stock_rooted_android_9.0_sdboot.img.gz) from _pine64.org_ (539MB, MD5 of the Gzip file _EE00D309745F842213E21B2F1E20C510_, build 20190621)

{{< admonition type="note" >}}
 Please unzip first and then using Android tool to flash it. Allow 3-5 minutes boot up time on first boot for initialization. The Rockchip SDDisk Tool ver. 1.57 can be found [here](https://files.pine64.org/os/ROCK64/android/SDDiskTool_v1.57.zip).
{{</ admonition >}}

### Android 8.x TV eMMC (preinstalled Google Play Store)

The *Android 8.1 TV* stock image for booting from the eMMC.

Image downloads (for direct flashing to the eMMC module):

* [Direct download](https://files.pine64.org/os/ROCK64/android/rock64_20180606_stock_android_8.1_emmcboot.img.xz) from _pine64.org_ (561MB, MD5 of the .xz file _C05846B89A6483DA911CEA604627524F_, build 20180606)

{{< admonition type="note" >}}
 Please allow 10-15 minutes boot up time on first boot for initialization.
{{</ admonition >}}

Image downloads (for Rockchip Tool):

* [Direct download](https://files.pine64.org/os/ROCK64/android/rock64_android8.1_emmc_boot_v1.1.zip) from _pine64.org_ (752MB, MD5 of the .xz file _9738F060D2F62A83637797363D2B38C9_, build 20180606)

{{< admonition type="note" >}}
 See the page about how to flash the eMMC using Rockchip Tools. Please unzip the file first and then use Rockchip tool to flash it. The OTG port located at top USB 2.0 port and it needs USB type A to type A cable.
{{</ admonition >}}

### Android 8.x TV

The *Android 8.1* stock image for microSD boot, build 20180623.

Download:

* [Direct download](https://files.pine64.org/os/ROCK64/android/rock64_20180623_stock_android_8.1_sdboot.img.xz) from _pine64.org_ (575MB, supports the microSD card)

{{< admonition type="note" >}}
 The MD5 hash of the .xz file is _85372A568C114ADE7CD9632CEBA193E9_
{{</ admonition >}}

Notes:

* Write the image to a microSD card using _dd_ and boot it.
* Please allow 10-15 minutes on first boot for initialization

### Android 7.x eMMC

The rooted _Android 7.1.2_ stock image, build 20171204.

Download image (microSD card to eMMC):

* [Direct download](https://files.pine64.org/os/ROCK64/android/rock64_20171204_stock_android_7.1.2_rooted_sd2emmc.img.xz) from _pine64.org_ (558MB, MD5 of the .xz file _43443467DFCAEDE767556843EB4D6707_)

{{< admonition type="note" >}}
 DD image to a microSD card. Shorting the eMMC PIN with a jumper as shown on the first image of the [guide to install stock Android build to eMMC module](https://files.pine64.org/doc/rock64/guide/ROCK64_Installing_Android_To_eMMC.pdf). After power ON the box for 2-3 second, quickly remove the jumper, then it will start writing the new image to the eMMC. Please allow around 1 minute of boot up time before UI is presented via HDMI. Please allow 10-15 minutes boot up time on first boot for initialization. Has USB 3.0 patches. Enable _Real Time Clock support_ for _Popcorn Hour Transformer_.
{{</ admonition >}}

Download image (eMMC boot):

* [Direct download](https://files.pine64.org/os/ROCK64/android/rock64_20171204_stock_android_7.1.2_rooted_emmc.img.xz) from _pine64.org_ (544MB, MD5 of the .xz file _7C831F9E6B4311A3B3D4743FBBB628D0_)

{{< admonition type="note" >}}
 Please unzip first and then using Android tool to flash in. Has USB 3.0 patches. Enable _Real Time Clock support_ for _Popcorn Hour Transformer_.
{{</ admonition >}}

Notes:

* See [MAC address](/documentation/ROCK64/Software/MAC_address) on how to set the MAC address.

### Android TV 7.x eMMC

The *Android TV 7.1* community build image by ayufan.

Download image (eMMC):

* [Direct download latest release build from ayufan github and look for android-7.1-rock-64-rock64_atv-x.x.x-xx-update.zip](https://github.com/ayufan-rock64/android-7.1/releases/latest)

{{< admonition type="note" >}}
 For eMMC flash-all image, please unzip first and then use Android tool to flash in
{{</ admonition >}}

Notes:

* Please allow 5 minutes boot up time on first time for initialization
* See [MAC address](/documentation/ROCK64/Software/MAC_address) on how to set the MAC address.
* [Release notes on ayufan Android 7.1 github](https://github.com/ayufan-rock64/android-7.1/releases/tag/0.3.4)

### Android TV 7.x

The *Android TV 7.1* community build image for microSD boot by _ayufan_.

Download:

* [Direct download latest release build from ayufan github and look for android-7.1-rock-64-rock64_atv-x.x.x-xx-raw.img.gz](https://github.com/ayufan-rock64/android-7.1/releases/latest) (supports the microSD card)

## Android SDK

The *Android P SDK* (v9.0).

Download:

* [Direct Download](https://files.pine64.org/SDK/ROCK64/ROCK64_SDK_android9.0.tar.gz) from _pine64.org_ (104.34GB)

{{< admonition type="note" >}}
 The MD5 hash of the TAR-GZip file is _1EAC08942E238293E3AF11C7890DF307_
{{</ admonition >}}

