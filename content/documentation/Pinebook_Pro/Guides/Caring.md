---
title: "Caring"
draft: false
menu:
  docs:
    title:
    parent: "Pinebook_Pro/Guides"
    identifier: "Pinebook_Pro/Guides/Caring"
    weight:
---

## Bypass Cables
	
{{< admonition type="warning" >}}
 Do not connect the bypass cables with the battery connected. Using the bypass cables with the battery connected can permanently damage your Pinebook Pro. After you’re done with using the bypass cables and want to return to the default setup, make sure to affix the bypass cables to the main body of the laptop using adhesive tape, in the same way as it was done in the factory. This ensures that the exposed leads in the connectors on the bypass cables don’t touch any conductive surface inside the laptop, which may cause a short.
{{</ admonition >}}

The mainboard features two bypass cables that are to be used only with the battery disconnected. The two bypass cables are disconnected by default. The female (10) male (6) ends of the bypass cables can be connected to provide power to the mainboard if you need to run your Pinebook Pro with no battery. Please refer to this [engineering notice](https://files.pine64.org/doc/PinebookPro/PinebookPro_Engineering_Notice.pdf) for more details.

Connecting the bypass cables together effectively connects the charger input where the battery output is, which also bypasses the charging circuit inside the Pinebook Pro. Thus, with the bypass cables connected together, the charger powers the Pinebook Pro directly, just like the battery does it when the laptop is running on battery power. This also means that no input current limiting is any longer in place, making it possible to draw more than 3&nbsp;A from the charger, and to trigger its overcurrent protection, which may cause operating system instability and crashes.

Despite the bypass cables having two conductors, they are used as a single conductor. Having both wires soldered together on either side of the bypass cables is normal, and such load-sharing design allows use of a compact connector on the bypass cables.

When removing the large RF shield found on the mainboard, for example when shorting the pins on the SPI chip, make absolutely sure to align it correctly while putting it back. Failing to do so can result in shorting the battery to the ground, due to the close proximity of the solder pads for the bypass cables, which would prevent the normal operation and effectively cause a fire hazard. It is highly recommended to disconnect the battery before removing the RF shield, and before putting it back.

## Guides

These are self-service instruction guides for the disassembly of the 14-inch Pinebook, but they still almost directly apply to the Pinebook Pro:

* [Lithium Battery Pack Removal Guide](https://files.pine64.org/doc/pinebook/guide/Pinebook_14-Battery_Removal_Guide.pdf)
* [LCD Panel Screen Removal Guide](https://files.pine64.org/doc/pinebook/guide/Pinebook_14-Screen_Removal_Guide.pdf)
* [eMMC Module Removal Removal Guide](https://files.pine64.org/doc/pinebook/guide/Pinebook_14-eMMC_Removal_Guide.pdf)

Assembling it back requires the described steps to be performed in the reverse order.
