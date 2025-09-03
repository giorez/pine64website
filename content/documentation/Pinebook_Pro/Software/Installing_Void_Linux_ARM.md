---
title: "Installing Void Linux ARM"
draft: false
menu:
  docs:
    title:
    parent: "Pinebook_Pro/Software"
    identifier: "Pinebook_Pro/Software/Installing_Void_Linux_ARM"
    weight:
aliases:
  - /wiki/Pinebook_Pro_Installing_Void_Linux_ARM
  - /wiki/Installing_Void_Linux_ARM_On_The_Pinebook_Pro
---

{{< admonition type="warning" >}}
 This guide is a Work In Progress; no warranty is implied. This installation method is not officially recommended (or discouraged) by the Void Linux project. This guide is for experienced Linux users.
{{</ admonition >}}

This will not be a complete guide, as it borrows heavily on [Installing Arch Linux ARM](/documentation/Pinebook_Pro/Software/Installing_Arch_Linux_ARM), so read it first then come back here.

Only the steps that are different are listed here. Be careful, the numbering of the sections is not the same.

## Installing the root filesystem

### Downloading and verifying the rootfs tarball

You can go to the Void Linux [download page](https://voidlinux.org/download/), select the "arm" tab, and choose one of the aarch64 rootfs tarballs, either glibc or musl.
How to check integrity of the downloaded file is explained on the same page.

Or use the following instructions (on Debian):

```console
$ wget https://repo-default.voidlinux.org/live/current/void-aarch64-musl-ROOTFS-20221001.tar.xz
$ wget https://repo-default.voidlinux.org/live/current/sha256sum.{txt,sig}
$ wget https://github.com/void-linux/void-packages/raw/master/srcpkgs/void-release-keys/files/void-release-20221001.pub
$ signify-openbsd -V -p void-release-20221001.pub -x sha256sum.sig -m sha256sum.txt
Signature Verified
$ sha256sum -c --ignore-missing sha256sum.txt
void-aarch64-musl-ROOTFS-20221001.tar.xz: OK
```

### Extracting and configuring the root filesystem

#### Extracting the root filesystem

    tar -xpf void-aarch64-musl-ROOTFS-20221001.tar.xz -C /mnt

#### Kernel

The Void Linux rootfs tarball does not contain a kernel, however  the **pinebookpro-kernel** package can be installed from the Void Linux repositories. Alternatively, one can (cross) build a kernel themselves. Skip this section if you would rather install the package.

{{< admonition type="warning" >}}
 If you choose the manually built kernel route, you’ll have to keep it updated yourself, the same way: manually (cross-)building and installing.
{{</ admonition >}}

##### Manually cross-compiling a mainline kernel suitable for the Pinebook Pro

We’ll use the postmarketOS kernel configuration and boot parameters, because they are working properly, and are sufficiently up-to-date. This is done from an x86_64 computer.

This has been tested with postmarketOS configuration for 6.0.2 and kernel 6.1.0-rc5+. No additional initramfs was needed to boot the Void Linux OS.

```console
$ git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
$ cd linux
$ wget -O .config 'https://gitlab.com/postmarketOS/pmaports/-/raw/master/device/community/linux-postmarketos-rockchip/config-postmarketos-rockchip.aarch64?inline=false'
$ sed -i \
  -e 's|CONFIG_ROCKCHIP_CDN_DP=.*|CONFIG_ROCKCHIP_CDN_DP=n|' \
  -e 's|CONFIG_BATTERY_CW2015=.*|CONFIG_BATTERY_CW2015=y|' \
  -e 's|CONFIG_TYPEC_FUSB302=.*|CONFIG_TYPEC_FUSB302=y|' \
  -e 's|CONFIG_TYPEC_TCPM=.*|CONFIG_TYPEC_TCPM=y|' \
  .config
$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j1 oldconfig
$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(grep -c '^processor' /proc/cpuinfo)
```

##### Manually installing the newly built kernel, modules & DTB files

```console
$ KVER="$(make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j1 kernelrelease)"
$ sudo make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j1 modules_install dtbs_install \
		INSTALL_MOD_STRIP=1 \
		INSTALL_MOD_PATH=/mnt \
		INSTALL_DTBS_PATH=/mnt/boot/dtbs
$ sudo cp arch/arm64/boot/Image "/mnt/boot/Image-${KVER}"
```

#### Configuring a login agent on the serial console

```console
cp -R /mnt/etc/sv/agetty-ttyS0 /mnt/etc/sv/agetty-ttyS2
ln -sf /etc/sv/agetty-ttyS2 /mnt/etc/runit/runsvdir/default
```

#### Creating extlinux.conf

{{< admonition type="note" >}}
If using the official PBP kernel package, it is also recommended to use the **u-boot-menu** package, which automatically regenerates the extlinux.conf file on kernel upgrades. In that case, you will not need to follow the below instructions.
{{</ admonition >}}

The following borrows from [postmarketOS u-boot configuration for the kernel command-line parameters](https://gitlab.com/postmarketOS/pmaports/-/blob/master/device/community/device-pine64-pinebookpro/extlinux.conf).

We force the serial console to 115200 bauds (from the default 1.5M bauds), so that it is the same as tow-boot’s.

```
# mkdir -p /mnt/boot/extlinux
# cat <<EOF > /mnt/boot/extlinux/extlinux.conf
default l0
menu title Pinebook Pro Boot Menu
prompt 0
timeout 50

label l0
menu label Boot Kernel on SD
linux /Image-${KVER}
fdt /dtbs/rockchip/rk3399-pinebook-pro.dtb
append console=tty0 console=ttyS2,115200n8 coherent_pool=1M pcie_aspm.policy=performance video=HDMI-A-1:1920x1080@60 video=eDP-1:1920x1080@60 rw rootwait root=/dev/mmcblk1p3
EOF
```

### Finalizing

Now you can umount the partition(s) and boot the Pinebook Pro with Void Linux. The default root password is "voidlinux".
