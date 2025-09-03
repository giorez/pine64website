---
title: "Installation to the microSD card"
draft: false
weight: 
menu:
  docs:
    title:
    parent: "PinePhone/Installation"
    identifier: "PinePhone/Installation/Installation_to_the_microSD_card"
    weight: 2
---

For this installation method you need a **microSD card**, a **microSD card reader** and a **compatible device**, such as a computer or a laptop with Linux, iOS, Windows or similar (note: ChromeOS is not supported).

To install an image to the microSD card:

1. Download your chosen image from [Releases](/documentation/PinePhone/Software/Releases) for the regular **PinePhone** (not compatible with the PinePhone Pro).
2. Extract the compressed file
3. Write (_flash_) the image to your microSD card, see the instructions below
4. Plug microSD card into phone (make sure to use the top slot, not the bottom slot)
5. Boot up the phone

{{< figure src="/documentation/images/Pinephone_slots.png" caption="The microSD belongs in the upper slot, the micro-SIM in the lower slot." width="600" >}}

## Using Balena Etcher

Using the graphical application _Balena Etcher_ to flash the microSD card is _'recommended_' for new or inexperienced users.

Download and install the application: https://etcher.balena.io/#download-etcher

Then start it and click the button _Flash from file_:

{{< figure src="/documentation/PinePhone/Installation/Etcher1.png" width="600" >}}

Select the downloaded image and make sure that you downloaded the correct one. Images for the PinePhone and the PinePhone Pro are _'not compatible_' with each other. Images for the PinePhone typically have the word "PinePhone" in the filename, while images for the PinePhone Pro typically have "PinePhone Pro" in their filename.

{{< admonition type="note" >}}
 At this the image file does not have to be extracted from the archive format. Balena Etcher handles the extracting automatically.
{{</ admonition >}}

Then click on _Select target_:

{{< figure src="/documentation/PinePhone/Installation/Etcher3.png" width="600" >}}

{{< admonition type="note" >}}
 Make sure to select the correct target by comparing the name and the disk capacity with the label on the microSD card.
{{</ admonition >}}

Then click on _Flash!_:

{{< figure src="/documentation/PinePhone/Installation/Etcher4.png" width="600" >}}

That’s it!

## Using dd

For flashing the microSD card, the command _dd_ can be used as well.

Make sure to select the correct device using `lsblk`. Then run _dd_ with the selected device:

`sudo dd if=IMAGE.img of=/dev/[DEVICE] bs=1M status=progress conv=fsync`

{{< admonition type="note" >}}
 The image needs to be written to the whole device, not to partition 1. Make sure you’re NOT selecting _/dev/sda1_ or _/dev/mmcblk0p1_ as target.
{{</ admonition >}}

## Using bmaptool

Make sure to select the correct device using `lsblk`. Then run bmaptool with the correct device:

Download the _IMAGE.xz_ and the _IMAGE.bmap_ files, then run:

`bmaptool copy --bmap IMAGE.bmap IMAGE.xz /dev/[DEVICE]`

This takes around 2.5 minutes to flash a 4 Gb file.

## Using Gnome Disks

The graphical application _Gnome Disks_ can be used to flash the microSD card as well.

To do so, select the correct device in the left device selection, then click on the three dot menu and select _Restore Disk Image..._ and follow the on-screen instructions.
