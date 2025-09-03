---
title: "Software"
draft: false
menu:
  docs:
    title:
    parent: "Pinebook"
    identifier: "Pinebook/Software"
    weight: 3
aliases:
  - /wiki/Pinebook_Software_Release
  - /wiki/Pinebook_Software_Releases
  - /wiki/1080P_Pinebook_Software_Release
  - /wiki/1080P_Pinebook_Software_Releases
---

This page contains a list of all available releases and tools for the [Pinebook](/documentation/Pinebook).

## Linux

### AOSC

{{< figure src="/documentation/images/aosc.png" width="100" >}}

**AOSC OS** is a general purpose Linux distribution that strives to simplify user experience and improve free and open source software for day-to-day productivity. To learn more about AOSC, please visit the official [AOSC website](https://aosc.io/).

Download:

* https://aosc.io/downloads/

| Default credentials | |
| --- | --- |
| `aosc` | `anthon` |

### Armbian

{{< figure src="/documentation/images/armbian.png" width="100" >}}

**Armbian** is a Linux distribution designed for ARM boards. They are usually Debian or Ubuntu flavored. To find out more about Armbian and available download options please visit the [Armbian ROCK64 site](https://www.armbian.com/rock64/).

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ✅ | ✅ |

Download:

* https://www.armbian.com/pinebook-a64/

| Default credentials | |
| --- | --- |
| `root` | `1234` |

### Debian

**Debian** is an operating system and a distribution of Free Software. The forum thread for release can be found [here](https://forum.pine64.org/showthread.php?tid=14341).

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ✅ | ✅ |

Download:

* [Debian 11 Bullseye](https://deb.debian.org/debian/dists/bullseye/main/installer-arm64/current/images/netboot/SD-card-images/) (recommended)
* [Debian 12 Bookworm](https://deb.debian.org/debian/dists/bookworm/main/installer-arm64/current/images/netboot/SD-card-images/)
* [Daily netboot images](https://d-i.debian.org/daily-images/arm64/)

Installation:

* The [Readme](https://d-i.debian.org/daily-images/arm64/daily/netboot/SD-card-images/README.concatenateable_images) provides info about concatenating [firmware.pinebook.img.gz](https://d-i.debian.org/daily-images/arm64/daily/netboot/SD-card-images/firmware.pinebook.img.gz) + [partition.img.gz](https://d-i.debian.org/daily-images/arm64/daily/netboot/SD-card-images/partition.img.gz) to create a bootable installer image.

Notes:

* Installer offers automatic partitioning and full-disk encryption (LUKS), but only manual partitioning with a single ext4 partition has been confirmed to work.
* Bootloader must be installed separately after installation, before rebooting.
* WiFi driver kernel module must be provided during installation, or a USB network adapter used. (Android USB tethering works, with network driver `rndis_host`).
* See also: Debian Netboot installer on the 1080P Pinebook under [Software releases](/documentation/Pinebook_Pro/Software/Releases#debian)

### DietPi

{{< figure src="/documentation/images/dietpi.png" width="100" >}}

**DietPi** is a lightweight yet easy to setup and feature-rich Linux distribution, based on Debian. To find out more about DietPi, please visit the [official documentation](https://dietpi.com/docs/). Discuss the ROCK64 build on the [PINE64 forum thread](https://forum.pine64.org/showthread.php?tid=12512).

Download:

* [Debian 11 Bullseye](https://dietpi.com/downloads/images/DietPi_Pinebook-ARMv8-Bullseye.img.xz) (supports the microSD card and eMMC, 4GB or more)
* [Debian 12 Bookworm](https://dietpi.com/downloads/images/DietPi_Pinebook-ARMv8-Bookworm.img.xz) (supports the microSD card and eMMC, 4GB or more)

| Default credentials | |
| --- | --- |
| `root` | `dietpi` |

### Kali

{{< figure src="/documentation/images/Kali-logo.png" width="100" >}}

**Kali Linux** is an Advanced Penetration Testing Linux distribution used for Penetration Testing, Ethical Hacking and network security assessments.

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ✅ | ✅ |

Download:

* https://www.kali.org/get-kali/#kali-arm

| Default credentials | |
| --- | --- |
| `kali` | `kali` |

### Slackware

{{< figure src="/documentation/images/slackware.jpg" width="100" >}}

**Slackware** is a very old, interesting, convenient and easy distribution. Visit the project’s website here (https://fail.pp.ua). You can follow the ongoing discussion about Slackware on the PINE64 forum (https://forum.pine64.org/showthread.php?tid=9439).

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ❓ | ✅ | ❓ |

Download:

* [Direct download from developer KRT site and look for slarm64-current-aarch64-xfce-rootfs-xxxxxxxx-x.x.xx-pinebook-build-xxxxxxxx.img.lrz](https://3space.xyz/pineslarm/)

| Default credentials | |
| --- | --- |
| Root user |
| `root/password` |

## BSD Image Releases

### NetBSD

{{< figure src="/documentation/images/netbsd.png" width="100" >}}

NetBSD community build. To learn more about NetBSD please visit the [NetBSD main page](https://www.netbsd.org/).

Download:

* [Direct download latest release build from NetBSD by select 64bit - Pinebook](https://nycdn.netbsd.org/pub/arm/)

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ❓ | ❓ |

Notes:

* Instructions concerning enabling SSH can be found [here](https://www.netbsd.org/docs/guide/en/chap-boot.html#chap-boot-ssh)

| Default credentials | |
| --- | --- |
| `root` (SSH and TTY)| `[none]` |

### OpenBSD

{{< figure src="/documentation/images/Puffy_mascot_openbsd.png" width="100" >}}

OpenBSD 6.6-snapshot, Community Build Image (FVWM2 WM). To learn more about OpenBSD please visit [OpenBSD main page](https://www.openbsd.org). If you need more information please ping: https://forum.pine64.org/member.php?action=profile&uid=12423.

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* SHA256: [Community member elewarr’s Dropbox](https://www.dropbox.com/s/79hpdpehrbbk984/pinebook-2019-11-04.img.tgz.sha256?dl=0)
* Image: [Community member elewarr’s Dropbox](https://www.dropbox.com/s/yas1glfvvucb9a0/pinebook-2019-11-04.img.tgz?dl=0)

| Default credentials | |
| --- | --- |
| `pine64` (SSH and TTY) | `pine64` |
| `root` | `pine64` |

## Android Image Releases

{{< figure src="/documentation/images/Android_logo_2019_(stacked).svg" width="100" >}}

### Android 7.x

Android 7.1 Community Build Image [microSD Boot] by ayufan. It only works on the 14.1" and 11.6" Pinebook, not applicable to 1080P 11.6' Pinebook. Special thanks to ayufan, Icenowy, lennyraposo, longsleep, lukasz, tkaiser, Xalius and PINE64 community contributors. Please use good random IO access performance microSD card such as the _Samsung EVO_ when trying out Android 7.1.

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [ayufan’s GitHub](https://github.com/ayufan-pine64/android-7.1/releases/latest), look for _android-7.1-pine-a64-pinebook-x.x.x-xx.img.gz_ (for microSD cards with 4GB or more)

Notes:

* Please allows some time (around 5 minutes) for the initialization process on the first boot.

### Android 6.x eMMC

#### Android 6.0.1

Rootable build, online update (OTA) only works when the build is not rooted. The LCD resolution is 1366 x 768.

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ❌ | ✅ |

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Rooted image (for microSD cards with 4GB or more)](https://files.pine64.org/os/Pinebook/android/android-ver6.0.1-rooted-20170605-pinebook-sd2emmc-lpddr3.img.xz) from _pine64.org_ (776MB, MD5 of the Gzip file _C99BF459C6724BA73F12C532E87A8BA5_, build 20170605)

Notes:

* microSD to eMMC

#### Android 6.0.1

Rootable build. The LCD resolution is 1920 x 1080.

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ❌ | ✅ | ❌ |

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Rooted image (for microSD cards with 4GB or more)](https://files.pine64.org/os/Pinebook/android/android-ver6.0.1-rooted-20181001-1080P-pinebook-sd2emmc-lpddr3.img.gz) from _pine64.org_ (595MB, MD5 of the Gzip file _E433A148CEBD743EADE6CAA765331A4B_, build 20181001)

Notes:

* microSD to eMMC

#### Android 6.0.1

Rootable build. The LCD resolution is 1920 x 1080. Please use an high performance microSD card for Android. Please ignore the warning message regarding an corrupted SD on the home screen in the upper left corner.

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ❌ | ✅ | ❌ |

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [For 8GB microSD cards](https://files.pine64.org/os/Pinebook/android/android-rooted-ver6.0.1-20181001-1080P-pinebook-sdboot-lpddr3-8GB.img.gz) from _pine64.org_ (553MB, MD5 of the Gzip file _CD27DF6083E6A4A5E7C8B986EB92FAA7_, build 20181001)
* [For 16GB microSD cards](https://files.pine64.org/os/Pinebook/android/android-rooted-ver6.0.1-20181001-1080P-pinebook-sdboot-lpddr3-16GB.img.gz) from _pine64.org_ (703MB, MD5 of the Gzip file _1376AAE8382E96FD7B45B0998A5CD6E9_, build 20181001)
* [For 32GB microSD cards](https://files.pine64.org/os/Pinebook/android/android-rooted-ver6.0.1-20181001-1080P-pinebook-sdboot-lpddr3-32GB.img.gz) from _pine64.org_ (867MB, MD5 of the Gzip file _B54E7F323B316750654E385B078AEC58_, build 20181001)
* [For 64GB microSD cards](https://files.pine64.org/os/Pinebook/android/android-rooted-ver6.0.1-20181001-1080P-pinebook-sdboot-lpddr3-64GB.img.gz) from _pine64.org_ (734MB, MD5 of the Gzip file _C8DBC6293EB51E58F91E27364C8C587D_, build 20181001)

Notes:

* microSD boot

### /e/

{{< figure src="/documentation/images/e.png" width="100" >}}

/e/OS community build. To learn more about /e/OS, please visit the [official website](https://e.foundation/). Please check out [this article](https://medium.com/@edevelopers.blog/e-os-ports-for-the-pinebook-and-pinephone-596139c76479) on the Pinebook /e/ build. For a thread discussion please visit the [PINE64 forum](https://forum.pine64.org/showthread.php?tid=7954)

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ❌ | ✅ | ❌ |

{{< admonition type="warning" >}}
 Outdated release
{{</ admonition >}}

Download:

* [Direct download from pine64.org](https://files.pine64.org/os/Pinebook/e/e-n-pinebook_20190926.gz) (685MB, MD5 of the GZip file: _4DC46A4E3ED2B47F4830E96DFCBBC6D8_)

## Linux BSP SDK

Download:

* [Linux BSP 4.0](https://files.pine64.org/os/sdk/A64-ver4.0/A64-BSP-4.0.tar.gz) from _pine64.org_ (4.67GB, MD5 of the TAR-GZip file _802D7C92D27177CBD17567359F9845A7_)
* [Linux BSP 3.0](https://files.pine64.org/os/sdk/A64-ver3.0/A64-BSP-3.0.tgz) from _pine64.org_ (4.18GB, MD5 of the TAR-GZip file _898ACF446851DF3BE7B643F62CE3CE84_)
* [Linux BSP 2.0, kernel v3.10 (including GPL compliance header)](https://files.pine64.org/os/sdk/A64-ver2.0/A64-BSP-2.0-GPL.tar.gz) from _pine64.org_ (6.41GB, MD5 of the TAR-GZip file _2EE11C9AED246C17995493F213A6A6DA_)

## Android SDK

Android Marshmallow (v6.0)

Download:

* [Direct Download](https://files.pine64.org/SDK/Pinebook/Pinebook_SDK_android6.0.tar.xz) from _pine64.org_ (15.92GB, MD5 of the Zip file _12362D0B63EBF29FC363A50A942346D5_)

| Compatibility | | |
| --- | --- | --- |
| Pinebook 11.6″ | Pinebook 11.6" 1080p | Pinebook 14″ |
| ✅ | ❓ | ❓ |

## Other resources

* Mali_Driver
* [Allwinner PhoenixCard Bootable SD-Card Creator](https://drive.google.com/file/d/0B0cEs0lxTtL3VmstaEFfbmU1NFk/view?usp=sharing)
* [Allwinner DragonFace V2.2.5 software that will let you edit and modify A64 Android Build PhoenixCard image](https://chinagadgetsreviews.com/download-dragonface-latest-version-v-2-2-5.html) ([Direct download at Mega](https://mega.nz/#!QxEjmaKB!S5nsVnzXVZg5aJ6qLtPOx1yJDPlbl0Vs4iV9VliRpE8))
