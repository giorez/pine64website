---
title: "Extend partition"
draft: false
weight: 
menu:
  docs:
    title:
    parent: "PinePhone/Installation"
    identifier: "PinePhone/Installation/Extend_partition"
    weight: 5
---

Once you’ve flashed the OS to your microSD card or eMMC storage, you may also need to expand the partition to fill all the available space.

{{< admonition type="note" >}}
 Many operating systems already include a script, which is resizing the partition on first boot, where this step is not required.
{{</ admonition >}}

## Resize SD card's partition using computer

For microSD cards, insert the microSD card and resize the partitions through the computer. For eMMC, insert the phone cable and use Jumpdrive to access the eMMC directly, and resize the partition after flashing the image. To do the flashing you have two options:

### Using Growpart

Install _growpart_ and run:

```shell
growpart /dev/**mmcblkX** **Y**
resize2fs /dev/**mmcblkXpY**
```

where _X_ is the storage device and _Y_ is the partition number (viewable from `lsblk`).

If you get any errors about missing or unknown commands, use `apt-cache search` to find and install the needed software. Also don’t forget to use `sudo`.

### Using Parted

Parted’s interactive mode and resize work well together. Do this before you put your microSD card into the PinePhone for the first time for best results.

```shell
sudo parted /dev/*<your_sd_card_device>*
(parted) resizepart 2 100%
(parted) quit
sudo resize2fs /dev/*<the_second_sd_card_PARTITION>*
```

## Resize from within the PinePhone

eMMC: you would need to resize the partition on eMMC (flashed with the operating system) by booting another image from the microSD card: that way, the eMMC will be unmounted. It is **not recommended** to resize eMMC while booted from eMMC! Resizing a currently mounted partition can have weird results. If you booted from the microSD card, you can follow the above guidelines on how to resize from a computer.

MicroSD card: It is generally not possible to boot from eMMC to partition the unmounted microSD card, because of the boot order - you would have to write the image to the empty microSD card first, then resize partition, all without rebooting. It is also **not recommended** to resize the microSD card while booted from microSD card! Resizing a currently mounted partition can have weird results.
