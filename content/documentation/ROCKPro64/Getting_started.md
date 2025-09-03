---
title: "Getting started"
draft: false
menu:
  docs:
    title:
    parent: "ROCKPro64"
    identifier: "ROCKPro64/Getting_started"
    weight: 1
aliases:
  - /wiki/ROCKPro64_Getting_Started
---

This section gives important information to get the board up and running.

## Video Playback

Hardware video acceleration is supported in recent kernels and user needs only to install the relevant Mesa packages/ports, specifically the Mesa DRI drivers for Mali GPUs (Midgard/Bifrost). One can confirm via software glxinfo, or having the library file such as .../lib/dri/panfrost_dri.so.

Ayufan has some old documentation on [video playback here.](https://github.com/ayufan-rock64/linux-build/blob/master/recipes/video-playback.md) For your ROCKPro64 the install should be

`sudo apt-get install ffmpeg mpv libmali-rk-midgard-t86x-r14p0-gbm`

(These modules are included in the Ayufan desktop releases.) At which stage rkmpv myvideo.mp4 will play a fullscreen, hardware assisted, version of your video. rkmpv is at /usr/local/bin/rkmpv

## Using an NVMe Disk as rootfs

Forum member Bullet64 has documented [how to move rootfs to an NVMe disk.](https://forum.frank-mankel.org/topic/208/booten-von-der-nvme-platte) This is useful until we get a full SPI option to boot from the NVMe.

## Setup a Serial Console (UART2)

{{< admonition type="warning" >}}
 RockPro64 is designed to use 3VDC3A (3 Volts Direct Current 3 Ampere) for the connection, using 5VDC and more might damage the board!
{{</ admonition >}}

To use Serial Console you will a need operating system that supports it on your RockPro64, by default the serial console is provided for baud 9 600 which is far too slow for rockpro64 so consider using 1 500 000 (1.5Mbps) instead **IF** your serial console device supports it (many doesn’t which results in their inability to use the console).

{{< admonition type="warning" >}}
Do not connect RxD (pin 10) until the U-Boot SPL is running (see [RK3399 boot sequence](/documentation/General/RK3399_boot_sequence)) or the SPL will not start.

To avoid this issue, a simple [Serial Buffer Circuit](/documentation/ROCKPro64/Hardware/Serial_buffer_circuit) can be installed between the RockPro64 and the serial adapter.
{{</ admonition >}}

In terms of connections you need to perform the following from your serial console-capable device e.g. Pine64’s Woodpecker available in store:

* GND <-> GND (pin 6)
* RxD <-> TxD (pin 8)
* TxD <-> RxD (pin 10)

After the configuration of your preferred operating system you can connect to the serial console using any of these commands:

```
$ screen /dev/ttyUSB0 1500000

$ picocom /dev/ttyUSB0 -b 1500000

$ minicom -D /dev/ttyUSB0 -b 1500000
```

{{< admonition type="note" >}}
 You might need a root permission if your user is not in the appropriate user-group e.g. `dialup` on GNU/Linux
{{</ admonition >}}

Alternatively there is a detailed guide on forums: https://forum.pine64.org/showthread.php?tid=6387

GNU/Linux:

* With GNU/Linux on your RockPro64 the built-in support for serial console can be enabled by parsing parse e.g. `console=ttyS2,1500000n8` in the kernel command line, many distributions make this available by default, but consider verifying the contents of `/boot/extlinux/extlinux.conf` if you encounter issues.
* NOTE: the `n8` in the kernel argument means **no parity, 8 bits per character**

## Booting from USB or PXE

The default choice of boot device is first eMMC (if present) then SDcard. See [ROCKPro64](/documentation/ROCKPro64) under "jumpers" for details on adjusting this sequence.

It is possible to flash the SPI to extend the options for boot devices to USB drives or PXE. The preferred method is now the rock64_write_spi_flash.sh script (see useful scripts above).

Background info and historic details of this usage [can be found here.](https://github.com/ayufan-rock64/linux-build/blob/master/recipes/flash-spi.md)

## Booting from SPI using u-boot

{{< admonition type="warning" >}}
 idbloader is not open-source
{{</ admonition >}}

Always be prepared to recover from a broken SPI boot BEFORE flashing or you will end up with a broken boot.

In general the recovery is killswitching SPI through shorting pins 23 <-> 25 together and then loading u-boot from a storage device e.g. SD-card or eMMC where majority of GNU distributions e.g. Manjaro usually have u-boot packaged with the provided images.

Follow instructions in https://github.com/sigmaris/u-boot/wiki/Flashing-U-Boot-to-SPI#instructions-for-rockpro64

## Boot sequence

The RockPro64 boot sequence has been documented [here](https://github.com/sigmaris/u-boot/wiki/RockPro64-boot-sequence) by sigmaris.

## OTG Mode

You can boot your ROCKPro64 into OTG mode with the use of the Recover button (see switch 28 under [Layout#Switches](/documentation/ROCKPro64/Board/Layout#switches)). Note that there are 2 OTG ports on your ROCKPro64: the type-C USB 3 socket is definitely one. From the schematic it appears the USB 3 (type A) socket is the other, but this has yet to be confirmed.

The method is to power off the board. Then push and hold the Recover button and push and release the Power button.

* If you have an Ayufan bootable image in either the SD-card or eMMC then there are 4 OTG modes [described here](https://github.com/ayufan-rock64/linux-u-boot/commit/ea6efecdfecc57c853a6f32f78469d1b2417329b) including Android fastboot, RockUSB and MaskROM modes. Releasing the Recover button as soon as the white LED lights counts as 1 blink. Keeping it pressed you will get 2 blinks of the white LED etc. Once the board enters OTG mode the red LED will be lit. In mode 1 the boot and linux-root partitions of the card with the Ayufan image (partitions 6 & 7 of a Linux installation) are made available as devices. In all cases the USB device made available at the host has device ID 18d1:d00d.
* If you do not have an Ayufan image in either the SD-card or the eMMC, then neither white nor red LEDs will light, but the board will enter MaskROM mode where the USB device made available at the host has device ID 2207:330c.

## NVMe Drives

Please be aware that [the PINE64 SSD interface card](https://pine64.com/product/rockpro64-pci-e-x4-to-m-2-ngff-nvme-ssd-interface-card) is intended for use with NVMe devices. These can be identified by the fact they have a single (Key M) notch, e. g. the _WD Black_ devices.

While M2/NGFF SATA devices (with a Key B notch, typically have Key M as well) will physically fit, they will not work. e. g. _WD Blue_ devices.

## SATA Drives

SATA drives can be connected directly via the [ROCKPro64 PCIe interface card.](https://pine64.com/product/pcie-to-dual-sata-iii-interface-card/) Please note the card does not include the power cable - that is a [separate item.](https://pine64.com/?product=rockpro64-power-cable-for-dual-sata-drives) Equally you must be aware that connecting SATA drives in this manner means they will be drawing power from your ROCKPro64 - please ensure you are using a 5A or better power supply.

ExplainingComputers did a YouTube [ROCKPro64 PCIe SATA card review and tests using a Ubuntu console and OpenMediaVault.](https://www.youtube.com/watch?v=9CCQicHwfDI)

## Wi-Fi & Bluetooth Module

If you have bought the [Wi-Fi and Bluetooth module](https://pine64.com/product/rockpro64-1x1-dual-band-wifi-802-11ac-bluetooth-5-0-module) from the Pine store then instructions for connecting it can be found on the accessories page. **Please note that the 0.7.9 Ayufan’s Linux releases (August 2018) have deliberately DISABLED support for this module in the search for stability. It can be tested and used with the Android image.**

It can also be used on Manjaro by installing ap6256-firmware and wireless-regdb packages.

## 7" LCD Touch Screen

Instructions for connecting the [LCD touch screen](https://pine64.com/?product=7-lcd-touch-screen-panel) from the Pineare on the accessories page.

**Note at present (August 2018) this screen is only supported by the Android image.**

{{< admonition type="warning" >}}
 When using the touchscreen ensure the cables are properly connected and tightened down and that you do not let the metal backplate touch the SBC
{{</ admonition >}}

## RTC Battery Backup

The Pine store has a couple of options for RTC battery backups: a [AAA version here](https://pine64.com/product/rtc-backup-battery-holder-2-x-aaa) or a [CR-2032 version here.](https://pine64.com/product/rtc-backup-battery-holder-cr-2032). For the ROCKPro64, the backup plugs into the RTC connector, number 6 in the board layout diagram above, next to the USB3 and case screw point.
