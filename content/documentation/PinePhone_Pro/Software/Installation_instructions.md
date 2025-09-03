---
title: "Installation instructions"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone_Pro/Software"
    identifier: "PinePhone_Pro/Software/Installation_instructions"
    weight: 2
aliases:
  - /documentation/PinePhone_Pro/Installing_a_different_operating_system/ # Page was moved
---

The software releases can be installed (the process is being referred to as _flashing_) to the internal memory of the PinePhone Pro (the eMMC) or to an microSD card.

## Installation to the microSD card

The images can be installed to an microSD card and be booted from it. 

{{< figure src="/documentation/PinePhone_Pro/images/pinephone_slots.png" caption="The microSD belongs in the upper slot, the SIM in the lower slot." width="600" >}}

{{< admonition type="note" >}}
 Compared to installations to the eMMC, running operating systems from the microSD card is slower than to the eMMC due to the microSD card’s slower reading and writing speeds.
{{</ admonition >}}

To install an image to the microSD card:

1. Download a compatible image from [Releases](/documentation/PinePhone_Pro/Software/Releases).
2. **Important:** Typically the image will be compressed in an archive file to reduce the download size (such as _.gz_ or _.xz_). Extract the image from its archive file to get the file with the file extension _.img_.
3. Write the image to your microSD card using your favorite method, examples:
   * Using _dd_: On the device you’re flashing the microSD card from, find the correct device under `lsblk` and then flash the image to the microSD card using `sudo dd if=IMAGE.img of=/dev/[DEVICE] bs=1M status=progress conv=fsync` and make sure the target is the whole microSD card and not its first partition, _sdc1_ or _mmcblk0p1_ are wrong!
   * Using _bmaptool_: Make sure to select the correct device using `lsblk`. Then run bmaptool with the correct device: Download the _IMAGE.xz_ and the _IMAGE.bmap_ files, then run `bmaptool copy --bmap IMAGE.bmap IMAGE.xz /dev/[DEVICE]`. This takes around 2.5 minutes to flash a 4 GB file.
   * Using _a graphical tool_: A graphical tool such as Gnome Disks under Linux or Etcher under Windows may also be used.
4. Insert the microSD card into the top slot of the PinePhone Pro
5. Boot the device using the following method:
   * With **rk2aw** (as on the _Explorer Edition_ ordered after November 2023): boot the phone without any further action if the image includes a bootloader or one is installed to the eMMC (such as in the default installation).
   * With **Tow-Boot** (as on the _Explorer Edition_ ordered after July 2022): hold the _volume down key_ while booting.
   * With an **empty SPI** (like on the _Explorer Edition_ ordered between January and July 2022): hold the _RE_ button underneath the back cover while booting (or use the _volume down key_ if you flashed _Tow-Boot_).
   * On the **Developer Edition** (sold to selected developers only) there is no _RE_ button. Instead apply the bypass by shorting the testing pads while booting according to the datasheet.

## Installation to the eMMC

Installing an operating system to the eMMC (the internal memory of the PinePhone Pro) can either be done by booting an operating system from the microSD and by installing to the eMMC directly from the booted microSD card operating system (recommended) or by using _Tow-Boot_'s USB Mass Storage mode.

{{< admonition type="warning" >}}
 Many images don’t include a bootloader. If the SPI only contains _rk2aw_ (like phones ordered after November 2023) or is empty (like phones ordered between January and July 2022), the installation on the eMMC won’t boot. In these cases, it is required to install a bootloader (such as [Tow-Boot](/documentation/PinePhone_Pro/Software/Bootloaders/#tow-boot)) in order to get the phone to boot.
{{</ admonition >}}

### By booting a microSD card

The eMMC can be overwritten by booting an image from the microSD card and overwriting the eMMC from within that booted microSD card image.

This installation method is **recommended**.

1. Boot an operating system [from the microSD card](/documentation/PinePhone_Pro/Software/Installation_instructions/). If there is already a bootloader on the eMMC installed see the section [Boot order](/documentation/PinePhone_Pro/Software/Boot_order/) to bypass it.
2. Download or copy the desired image to the microSD card as file
3. Check if the eMMC appears under `lsblk`. If it doesn’t appear in the output of the command, the eMMC wasn’t initialized due to applying the above explained bypass method for a too long time during the boot
4. **Important:** Typically the image will be compressed in an archive file to reduce the download size (such as _.gz_ or _.xz_). Extract the image from its archive file to get the file with the file extension _.img_.
5. Flash the image file using `sudo dd if=IMAGE.img of=/dev/mmcblk2 bs=1M status=progress conv=fsync` (replace _IMAGE.img_ with the filename of the image you want to flash and make sure it has the file extension _.img_).
6. Reboot the PinePhone Pro

### By using Tow-Boot

The image can be written to the eMMC by using Tow-Boot’s USB Mass Storage mode.

This installation method is **not recommended**, as the USB connection can be unreliable and in some cases not work at all.

1. Pre-requirement: Tow-Boot must be installed on the SPI, eMMC or the microSD card
2. Power off the device
3. Power on the device and hold the _volume up_ key before and during the second vibration
4. The LED will turn blue if done successfully. This will only work if Tow-Boot is installed
5. When connecting the device to a computer via USB it will behave like an USB drive now
6. Check if the eMMC appears under `lsblk`, the output might look like the following:\
`mmcblk2      179:0    0 115.2G  0 disk`\
`├─mmcblk2p1  179:1    0   122M  0 part /boot`\
`└─mmcblk2p2  179:2    0 115.1G  0 part /`\
Note: In this example, **/dev/mmcblk2** is the device, while _mmcblk2p1_ and _mmcblk2p2_ are partitions of the device. The downloaded images are images from full devices, which means that the full device (_mmcblk2_ in this example) needs to be flashed. Ignore the partitions!
7. **Important:** Typically the image will be compressed in an archive file to reduce the download size (such as _.gz_ or _.xz_). Extract the image from its archive file to get the file with the file extension _.img_
8. Flash the image file using `sudo dd if=IMAGE.img of=/dev/DEVICE bs=1M status=progress conv=fsync` (replace _IMAGE.img_ with the filename of the image you want to flash and make sure it has the file extension _.img_ and replace _DEVICE_ with the correct device from the _lsblk_ command)
9. Reboot the PinePhone Pro
