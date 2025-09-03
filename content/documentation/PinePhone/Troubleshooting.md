---
title: "Troubleshooting"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone"
    identifier: "PinePhone/Troubleshooting"
    weight: 5
---

If the PinePhone is not booting from eMMC and/or microSD card anymore it can have two causes:

## The battery is drained

If the battery is fully drained, most operating systems and distributions won’t boot anymore. One of the exceptions which still boots is the utility _Jumpdrive_, which can usually be used to expose the eMMC and microSD card as drives to a USB-connected computer. Mind that JumpDrive won’t expose the eMMC and microSD card with a drained battery but it still can be flashed and booted from microSD card to confirm that the phone still functions and boots up fine. 

JumpDrive can be downloaded from [here](https://github.com/dreemurrs-embedded/Jumpdrive/releases/download/0.8/pine64-pinephone.img.xz) (not compatible with the PinePhone Pro!). 

{{< admonition type="note" >}}
 If JumpDrive boots and other releases do not boot, the battery is likely drained. In that case let it charge while running JumpDrive with a compatible charger for multiple hours and make sure to not fully drain the battery in the future anymore, as that significantly reduces the battery lifetime.
{{</ admonition >}}

Alternatively to testing JumpDrive, the issue can also be diagnosed by checking the battery charge. Simply remove the battery from the device and measure the voltage on the (+) and (-) contacts on the battery. Make sure to not shorten the contacts as shorting battery pins is a severe life and safety danger.

## The installation is corrupted or incorrect

If the installation of the prioritized boot medium is corrupted or incorrect, the PinePhone will not boot anymore. The following problems are common:

* The microSD card is in the wrong slot (see first time installation)
* The image file was flashed to partition 1 (example: _sdx1_, _nvme0x1p1_) instead of the whole device (example: _sdx_, _nvme0x1_)
* An image without bootloader was flashed (mind the _Tow-Boot_ bootloader requirements of _Mobian_ and _postmarketOS_)
* The operating systems got corrupted, for example after running updates (reflash the device, see [Installation instructions](/documentation/PinePhone/Installation_instructions))
* An incompatible image was flashed (make sure that the images are compatible. Images for the PinePhone Pro won’t boot on the PinePhone and vice versa. Check your invoice to see if you ordered a PinePhone or a PinePhone Pro).
