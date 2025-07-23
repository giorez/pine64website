---
title: "Hardware compatibility"
draft: false
menu:
  docs:
    title:
    parent: "ROCKPro64/Hardware"
    identifier: "ROCKPro64/Hardware/Hardware_compatibility"
    weight: 2
aliases:
  - /wiki/ROCKPro64_Hardware_compatibility
  - /wiki/ROCKPro64_Hardware_Accessory_Compatibility
---

Please contribute to the hardware compatibility page, which lists hardware which has been tested with the rockpro64, whether successful or not.

## Hardware compatibility
### PCIe devices

| Type | Make/Model | Hardware IDs | Kernel | Result | Notes | Tester |
| --- | --- | --- | --- | --- | --- | --- |
| NIC | Intel I350 Dual Port |  | Mainline-5.4 | good | SR-IOV fails |  |
| NIC | Intel I350 Quad Port |  |  | ?  |  |  |
| NIC | Intel X520 Dual Port | 8086:10fb | Mainline-5.6 | good | SR-IOV fails |  |
| NIC | Intel X550-T2 Dual Port | 8086:1563 | 5.15.0-trunk-arm64 (Debian) | good | netperf throughput in FW mode, 20 streams: between 4136-6613mb/s across use cases. |  |
| NIC | Intel 82571EB Dual Port (HP NC360T) |  | Mainline-5.6 | crash | kernel crash on boot |  |
| NIC | Intel 82575EB Dual Port (AOC-SG-I2) |  | Mainline-5.10 | crash | kernel crash on boot |  |
| NIC | Intel 82575/82576 | 8086:1521 | OpenWrt 21.02-rc1 ; 5.4.111-1 | good  | opkg: kmod-igb; [OpenWrt 21.02-rc1](/documentation/ROCKPro64/Software/Releases/#openwrt) 5.4.111-1; ~92.8 KB; Kernel modules for Intel(R) 82575/82576 PCI-Express Gigabit Ethernet adapters. |  |
| NIC | Aquantia 10GBps AQC107 | 1d6a:07b1 | Mainline 5.16 | good | Works perfectly out of the box. |  |
| GPU | nVidia GTX-645 |  | Mainline-5.4 | crash | BAR size too small, triggers PCIe error handling bug |  |
| PCIe Switch | PCIE-EUX1-04 Ver.002 |  | Mainline-5.4 | good |  |  |
| SATA Controller | ASM1062 4-Port |  | Mainline-5.6 | good | tested only with one disk attached |  |
| SATA Controller | ASM1062 (rev 02) 4-Port | 1d87:0100 | Ayufan-4.4.190 | good | tested with four disks, 3 in raid 5 |  |
| SATA Controller | IOCrest (Same as Syba?) SI-PEX40063 4-port, Marvell 88SE9235 chip | 1b4b:9235 | Debian unstable 5.7, 5.8 | good | Tested with two disks. SATA errors occurred with a WD Red drive in a cheap enclosure; resolved by connecting the same drive directly to the card. |  |
| SATA Controller | Ziyituod SATA Card ASM 1062+1093 6-Port | 1b21:0625 | Mainline-4.4 (armbian) | good | tested with 6 disks |  |
| SATA Controller | BEYMEI RAID 4-Port, Marvell 88SE9230 chip | 1b4b:9230 | Ayufan-5.6.0-1137 | good | Tested with 3 disks in RAID 5. I added pci=nomsi to /boot/extlinux/extlinux.conf kernel parameters and an udev rule before the disks were recognized: ACTION=="add", SUBSYSTEM=="pci", ATTR{vendor}=="0x1b4b", ATTR{device}=="0x9230", RUN+="/bin/bash -c 'echo %k > /sys/bus/pci/drivers/ahci/bind'" |  |
| SATA Controller | BEYIMEI SATA Card 6-Port, ASM1166 chip |  | 5.10.0-16-arm64 (Debian) | good | Tested with 4 disks. Built 2 separate software RAID-1 arrays without errors. Performance seems good enough for a NAS on gigabit LAN. |  |
| SATA Controller | PCE8SAT-A02 VER006S<br> 2 Lanes, 8-Port, ASM1166 chip<br> Odd because chip got only 6 ports? | 1b21:1166 | 6.1.50-current-rockchip64<br> Armbian 23.8.1 Bookworm | unstable | Tested with 3 disks in SW-RAID 5. After 10 hours of burn in test one disk dropped from system **and** RAID. Hotplug does not work. | User:JPT |
| SATA Controller | BEYIMEI SATA Card 2-Port, ASM1062 chip | 1b21:0612 | 5.10.0-19-arm64 (Debian) | good | Using with 2 SSDs in a software RAID-1 array (~190MB/sec for reading and writing) |  |
| SATA Controller | QNINE 4-Port, Marvell 88SE9215 chip |  | Ayufan-5.6.0-1137 | very slow | Tested with 3 disks in RAID 5. Top speeds were around 50 MiB/s but quickly dropped to below 2 MiB/s due to SATA CRC errors |  |
| SATA Controller | YUNKOZAND-PCIE1X-SATA4-9215, Marvell 88SE9215 chip | 1b4b:9215 (rev 11) | Armbian 24.11.1, Kernel 6.12.12-current-rockchip64 | good | Kernel driver in use: ahci Tested with 2 disks in RAID 1. Top speeds were around 100 MB/s | User:o1hitman1o |
| SATA Controller | DELOCK 90498, JMicron Technology Corp. JMB58x AHCI SATA controller | 197b:0585 | 5.18.0-0.bpo.1-arm64 (Debian bullseye + backports) | good, but… | Tested with 3 disks, two in RAID1, one standalone. u-boot-rockchip_2023.07 cannot initialize the controller to boot off it. | User:Lrissman<br> User:ChriChri |
| Host Bus Adapter | LSI SAS 9211-4i<br> SAS2008 chip, 4-Port SAS/SATA, PCI 2.0, 8 lanes | 1000:0070 | Ayufan-4.4.197 | good | tested with four disks attached |  |
| Host Bus Adapter | Fujitsu SAS MEGARAID LSI 2008B2<br> SAS2008 chip, 8-Port SAS/SATA, PCI 2.0, 8 lanes | TODO | 6.1.50-current-rockchip64<br> Armbian 23.8.1 Bookworm  | TODO | needs special MicroSAS cables. Must be flashed to HBA mode?<br> ordered, not yet received | User JPT |
| USB Controller | ASMedia Technology Inc. ASM1142 USB 3.1 Host Controller | 1b21:1242 | Mainline-5.15.0-rc5 | good  |  |  |
| DTMB Quad Tuner | TBS Technologies | TSS6514 | Mainline-5.10.21 | good | TV -> LAN streaming server, 7W idle, 8-10W with one FHD channel streaming |  |
| DVB-T2/C Quad Tuner | TBS Technologies | TBS6205 | 5.10.0-16-arm64 (Debian) | good | Working well with Tvheadend |  |
| DVB-S2 Dual Tuner | Digital Devices | Octopus CI S2 Pro | 6.1.42-rockchip64 (armbian) | good | All features are working flawlessly with the latest drivers from Digital Devices |  |

### NVMe SSD drives

| Type | Make/Model | Size | Hardware IDs | Kernel | Result | Notes | Power options<br> Active only | Save power setting? |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NVMe | Samsung 970 Evo | 500 GB |  | Mainline 5.6 | good | - | defaults | defaults |
| NVMe | Samsung 960 Evo | 500 GB | 144d:a804 | Mainline 5.13-rc4 | doesn’t work | Likely due to 64/32 BAR mismatch issue on Linux 5.11+ | defaults | defaults |

### USB hardware

| Type | Make/Model | Hardware IDs | Kernel | Result | Notes | Tester |
| --- | --- | --- | --- | --- | --- | --- |
| Zigbee Bridge | Conbee II  | 1cf1:0030 | 6.1.50-current-rockchip64<br> Armbian 23.8.1 Bookworm | good | seems to work fine | User JPT |

### USB C alternate mode DP

Note that only USB C alternate mode Display Port will pass video. Any HDMI, DVI or VGA port must be converted internally by the device from Display Port - or the device won’t work for video.

| Type | Make/Model | Hardware IDs | Kernel | Result | Notes |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

### eMMC / SD drives

| Type | Make/Model | Hardware IDs | Kernel | Read Speed | Write Speed | Result | Notes  |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

### Other hardware

| Type | Make/Model | Hardware IDs | Kernel | Result | Notes |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Limitations

### Older firmware overwrites actively used memory

Some people get system freeze when:

* use SATA disk with ROCKPro64 PCIe card (maybe on newer PCIe card ASM1062 vs ASM1061)
* or do read or write 4GB to the flash (not using PCIe)

If you connect the serial console you will see a Linux kernel oops: (a)synchronous external abort.

Both issues are in fact the same software BUG. There is no hardware problem. Currently, most OS do use uboot with a rockpro blob FW which use memory that Linux kernel is not aware of. 

People are currently fixing this BUG, but it may take some time. In the mean time, you can fix it manually.

The latest u-boot can boot the rockpro64 without any blobs from rockchip.

Install first arm-none-eabi-gcc and aarch64-linux-gnu-gcc compiler, then run the following commands:

Prerequisite packages (Debian/Ubuntu): `device-tree-compiler python gcc-arm-non-eabi flex bison gcc-aarch64-linux-gnu gcc make`

```shell
git clone https://github.com/ARM-software/arm-trusted-firmware.git atf
make -C atf CROSS_COMPILE=aarch64-linux-gnu- PLAT=rk3399 bl31
git clone https://gitlab.denx.de/u-boot/u-boot.git u-boot
cd u-boot/
git checkout v2020.01-rc5
make rockpro64-rk3399_defconfig
BL31=../atf/build/rk3399/release/bl31/bl31.elf make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu-
```

Which gives you idbloader.img and u-boot.itb. Copy them to the rockpro64, and run the following: (Or put your SD card into your PC)

```shell
sudo dd if=idbloader.img of=/dev/mmcblk0 seek=64
sudo dd if=u-boot.itb of=/dev/mmcblk0 seek=16384
sync
```

### PCIe Controller Hardware Error Handling Bug

There is an issue with the rk3399 pcie controller that is currently unmitigated:

* [LKML Original Thread](https://lore.kernel.org/linux-pci/CAMdYzYoTwjKz4EN8PtD5pZfu3+SX+68JL+dfvmCrSnLL=K6Few%40mail.gmail.com/)
* [LKML Additional Information](https://lkml.org/lkml/2020/4/6/320)

The rk3399 pcie controller throws either a synchronous abort or a SError when a pcie device sends an unknown message.

The error type is determined by which cpu cluster handles the message.

### Virtualization

The PCIe controller on the rk3399 is not behind an IOMMU. This means it is not possible to safely pass through PCIe devices to a virtual machine.
