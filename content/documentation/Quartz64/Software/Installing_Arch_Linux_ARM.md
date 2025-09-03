---
title: "Installing Arch Linux ARM"
draft: false
menu:
  docs:
    title:
    parent: "Quartz64/Software"
    identifier: "Quartz64/Software/Installing_Arch_Linux_ARM"
    weight:
aliases:
  - /wiki/Quartz64_Installing_Arch_Linux_ARM
  - /wiki/Installing_Arch_Linux_ARM_On_The_Quartz64
---

The articles explains the installation of Arch Linux ARM on the [Quartz64](/documentation/Quartz64).

Commands to be run as a normal user are prefixed with `$`, commands to be run as root are prefixed with `#`. We assume your target device is ***/dev/sdX***, adjust accordingly.

## Partitioning The Block Device

Here we assume your block device is ***/dev/sdX***, adjust as needed.

Create a new partition table:

```console
# parted -s /dev/sdX mklabel gpt
```

Create the partitions for loader and u-boot:

```console
# parted -s /dev/sdX mkpart loader 64s 8MiB
# parted -s /dev/sdX mkpart uboot 8MiB 16MiB
```

Create the partition for u-boot’s environment:

```console
# parted -s /dev/sdX mkpart env 16MiB 32MiB
```

Create the "efi" boot partition and mark it as bootable:

```console
# parted -s /dev/sdX mkpart efi fat32 32MiB 544MiB
# parted -s /dev/sdX set 4 boot on
```

Create the root partition:

```console
# parted -s /dev/sdX mkpart root ext4 544MiB 100%
```

### Creating The File Systems

Now create the file systems for boot and root:

```console
# mkfs.vfat -n "efi" /dev/sdX4
# mkfs.ext4 -L "rootfs" /dev/sdX5
```

## Fetching and Flashing U-Boot

For this we’ll use the precompiled idblock and u-boot from pgwipeout’s CI.

Go to https://gitlab.com/pgwipeout/quartz64_ci/-/pipelines and click the three dots, download the merge-job artifacts.

Unzip them:

```console
$ unzip artifacts.zip
```

Flash idblock.bin and uboot.img:

```console
# dd if=artifacts/idblock.bin of=/dev/sdX1
# dd if=artifacts/uboot.img of=/dev/sdX2
```

## Fetching The Root File System Tarball

Fetch the root filesystem tarball and the PGP signature

```console
$ wget -N http://os.archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz{,.sig}
```

Fetch the gpg keys:

```console
$ curl 'https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x68b3537f39a313b3e574d06777193f152bdbe6a6' | gpg --import=-
```

Compare the key ID provided in the above command with the one listed here: https://archlinuxarm.org/about/package-signing (Take good note of the domain and HTTPS)

Verify the tarball’s authenticity

```console
$ gpg --verify ArchLinuxARM-aarch64-latest.tar.gz.sig
```

{{< admonition type="important" >}}
 Do not skip verifying the authenticity. This is important. It also protects you from prematurely aborted transfers giving you a corrupt archive.
{{</ admonition >}}

## Installing The Root File System

```console
# mount /dev/sdX5 /mnt/alarm-root
# mkdir /mnt/alarm-root/boot
# mount /dev/sdX4 /mnt/alarm-root/boot
# bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C /mnt/alarm-root
```

### Editing fstab

Find your partition UUIDs for both partitions using `lsblk`:

```console
$ lsblk -o NAME,SIZE,MOUNTPOINTS,PARTUUID
```

In ***/mnt/alarm-root/etc/fstab***, put the lines

```
PARTUUID=_root-uuid-here_  /       ext4    defaults        0       1
PARTUUID=_boot-uuid-here_  /boot   vfat    defaults        0       2
```

with your UUIDs in place of the placeholder.

### Writing extlinux.conf

Create a ***/mnt/alarm-root/boot/extlinux/extlinux.conf*** with these contents:

```
default l0
menu title Quartz64 Boot Menu
prompt 0
timeout 50
 label l0
menu label Boot Arch Kernel
linux /Image
fdt /dtbs/rockchip/rk3566-quartz64-a.dtb
append initrd=/initramfs-linux.img earlycon=uart8250,mmio32,0xfe660000 console=ttyS2,1500000n8 root=LABEL=rootfs rw rootwait
```

#### For Model B

Kernel 5.18 and 5.19 do not yet have the Quartz64 Model B device tree, however, you can add it manually to your install and adjust ***extlinux.conf***:

Download it from here: https://overviewer.org/~pillow/up/5f1fabef1b/rk3566-quartz64-b.dtb (this is just linux-next with sd card speed changed to ***sd-uhs-sdr50***)

Copy it to ***/mnt/alarm-root/boot/dtbs/rockchip/rk3566-quartz64-b.dtb***

Then adjust your ***/mnt/alarm-root/boot/extlinux/extlinux.conf****'s **fdt*** line as follows:

```
fdt /dtbs/rockchip/rk3566-quartz64-*b*.dtb
```

### Finishing Up

Once done, unmount the partitions:

```console
# umount /mnt/alarm-root/boot
# umount /mnt/alarm-root
```

## Booting And Finishing Setup

Hook up your UART dongle to your Quartz64, open a serial terminal at 1.5mbauds. Install the SD card or eMMC module inside the Quartz64, and plug in the power.

Once you hit a login shell, log in as `root` with password `root` and run:

```console
# pacman-key --init
# pacman-key --populate archlinuxarm
```

You are now ready to use Arch Linux ARM! Either delete or rename (and move the homedir of) the `alarm` user, and you’re all set. Don’t forget to install things like `sudo` and setting up sudo groups and such.
