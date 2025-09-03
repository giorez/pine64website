---
title: "Releases"
draft: false
menu:
  docs:
    title:
    parent: "SOPINE/Software"
    identifier: "SOPINE/Software/Releases"
    weight: 1
aliases:
  - /wiki/SOPINE_Software_Release
  - /wiki/SOPINE_Software_Releases
---

Note that SOPINE images are also compatible with the PINE A64-LTS.

## Linux

### AOSC
{{< figure src="/documentation/images/aosc.png" >}}

AOSC OS is a general purpose Linux distribution that strives to simplify user experience and improve free and open source software for day-to-day productivity. To learn more about AOSC, please visit the official [AOSC website](https://aosc.io/).

Download:

* https://aosc.io/downloads/ (supports the microSD card and eMMC, 8GB or more)

| Default credentials | |
| -------- | ------- |
| `aosc` | `anthon` |

### Armbian
{{< figure src="/documentation/images/armbian.png" >}}

Armbian is a Linux distribution designed for ARM boards. They are usually Debian or Ubuntu flavored. 

Download:

* https://armbian.hosthatch.com/archive/pine64so/archive/

### FreedomBox
{{< figure src="/documentation/images/FreedomBox.jpg" >}}

FreedomBox is a private server for non-experts: it lets you install and configure server applications with only a few clicks. For more information about FreedomBox, please visit https://www.freedombox.org.

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Direct download from FreedomBox site](https://ftp.freedombox.org/pub/freedombox/hardware/pine64-lts/stable/freedombox-stable-free_buster_pine64-lts-arm64.img.xz) (418MB)

Notes:

* This is a headless build, not HDMI output.
* Please plug-in Ethernet cable first before initial power up. After power up for 10 minutes, using browser and type in https://fredombox.local to setup. Browser may warms for unsecure site and please proceed with exception.
* Freedom Manual: https://wiki.debian.org/FreedomBox/Manual

### LibreELEC
{{< figure src="/documentation/images/libreelec.jpg" >}}

LibreELEC is a "Just enough OS" Linux distribution combining the Kodi media center with an operating system.

Download:

* [Pine A64+ build direct download from Libreelec nightly](https://test.libreelec.tv/) (look for _LibreELEC-A64.arm-...-nightly-xxxxxxxx-xxxxxxx-pine64-lts.img.gz_)

Notes:

* Nightly build for microSD and eMMC boot.

### NEMS Linux
{{< figure src="/documentation/images/nems.jpg" >}}

NEMS stands for "Nagios Enterprise Monitoring Server" and it is a modern pre-configured, customized and ready-to-deploy Nagios Core image designed to run on low-cost micro computers. To find out more on NEMS Linux, please visit their [site](https://nemslinux.com/).

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Direct download from pine64.org](https://files.pine64.org/os/SOPINE/nems/NEMS_v1.5-SOPine-Build1.zip) (supports the microSD card, 16GB or more, MD5 of the xz file is _5ad0d684296d50b4c1fcbac6db205ae0_)
* [Download torrent seed from NEMS Linux](https://nemslinux.com/download/nagios-for-pine64.php) (supports the microSD card, 16GB or more, MD5 of the xz file is _6e2088922c5d197db8b8ba3057120389_)

{{< admonition type="info" >}}
The installation guide can be found [here](https://docs.nemslinux.com/installation).
{{</ admonition >}}

| Default credentials | |
| -------- | ------- |
| `nemsadmin` | `nemsadmin` |

### OpenEmbedded
{{< figure src="/documentation/images/openembedded.png" >}}

OpenEmbedded is the build framework for embedded Linux. OpenEmbedded offers a best-in-class cross-compile environment. It allows developers to create a complete Linux Distribution for embedded systems. See https://www.openembedded.org/wiki/Main_Page for more information on OpenEmbedded.

Download:

* https://github.com/alistair23/meta-pine64/

Notes:

* OpenEmbedded/Yocto layer for the Pine64 boards 
* This layer aims to support as many features as possible on Pine64 devices. Where possible the layer aims to use opensource and upstream projects avoiding custom forks and binary solutions.
* More information and instructions can be found in the repo readme: https://github.com/alistair23/meta-pine64/#building

### OpenWRT
{{< figure src="/documentation/images/Openwrt_logo_square.png" >}}

OpenWRT community build for microSD boot. The OpenWrt Project is a Linux operating system targeting embedded devices.

Download:

* [Direct download](https://downloads.lede-project.org/snapshots/targets/sunxi/cortexa53/) (look for _pine64_sopine-baseboard-ext4-sdcard.img.gz_ and _pine64_sopine-baseboard-squashfs-sdcard.img.gz_)

Notes:

* This is headless build, please use serial console to configure

| Default credentials | |
| -------- | ------- |
| Default user | `-/passwd` |

## BSD

### NetBSD
{{< figure src="/documentation/images/netbsd.png" >}}

NetBSD is a free, fast, secure, and highly portable Unix-like Open Source operating system. To learn more about NetBSD please visit [NetBSD main page](https://www.netbsd.org/). 

Download:

* [Direct download](https://nycdn.netbsd.org/pub/arm/) (select _PINE A64-LTS / SoPine with baseboard_)

| Default credentials | |
| -------- | ------- |
| `root` (root user and SSH) | `[none]` |

Notes:

* NetBSD community build for microSD boot
* Instructions concerning enabling SSH can be found [here](https://www.netbsd.org/docs/guide/en/chap-boot.html#chap-boot-ssh)

## Linux BSP SDK

Linux BSP Kernel 4.9

Download:

* [Direct Download](https://files.pine64.org/SDK/PINE-A64/PINE-A64_lichee_BSP4.9.tar.xz) from _pine64.org_ (5.40GB, MD5 of the TAR-GZip _7736e3c4d50c021144d125cc4ee047a4_)

## Android SDK
Android Oreo (v8.1)

Download:

* [Direct Download](https://files.pine64.org/SDK/PINE-A64/PINE-A64_SDK_android8.1.tar.xz) from _pine64.org_ (24.94GB, MD5 of the TAR-Gzip _b0394af324c70ce28067e52cd7bc0c87_)
