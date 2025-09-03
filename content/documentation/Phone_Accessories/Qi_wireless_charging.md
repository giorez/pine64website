---
title: "Qi Wireless Charging Add-on"
draft: false
menu:
  docs:
    title:
    parent: "Phone_Accessories"
    identifier: "Phone_Accessories/Qi_wireless_charging"
    weight: 6
---

{{< admonition type="warning" >}}
Possible safety hazard: If the wireless charging chip fails for some reason, do not plug the phone in to charge via USB-C. Take the back case off first. It is possible that power gets fed into the chip, causing it to overheat, possibly causing damage to the phone and creating a fire-hazard.

Album of damage caused by reverse current: https://imgur.com/a/dJsp5wD

Until the cause of this is determined, it is recommended NOT to use the wireless charging add-on.
{{</ admonition >}}

{{< figure src="/documentation/images/PinePhone-Wireless-charger.jpg" width="250" >}}

Uses the pogo pins to supply Qi Wireless and Wireless Power Consortium compatible charging. No software required.

## Schematics and Datasheet

Schematic:

* [PinePhone Wireless Charger Back Cover Schematic ver 1.0 20210508](https://files.pine64.org/doc/PinePhone/PinePhone%20Q-Wireless%20Charger%20Back%20Cover%20Schematic-20210508.pdf)

Datasheet:

* [HL6111RFNWP5 5W WPC Wireless Power Receiver Datasheet](https://files.pine64.org/doc/datasheet/pinephone/HL6111RFNWP5_V1p0_20190121.pdf)
