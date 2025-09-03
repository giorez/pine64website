---
title: "Battery"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone"
    identifier: "PinePhone/Battery"
    weight:
---

The phone ships with a protective plastic sticker between the battery and the phone to protect the device from turning on during shipping. You need to gently open the back cover, then remove the battery and finally remove the sticker and check that the pins aren’t bent. Note: If the battery is stuck inside the phone, the mid screw in the lower part of the midframe needs to be slightly loosened, see [here](/documentation/PinePhone/FAQ#the_battery_is_stuck_inside_the_phone).

{{< admonition type="note" >}}
 The EG25-G modem and the RTL8723CS WiFi and Bluetooth do not work without a battery and with a drained battery, even when enough power is supplied to the PinePhone via the USB Type-C port. Most operating systems won’t boot without a battery or with a drained battery.
{{</ admonition >}}

The [supplied battery](https://files.pine64.org/doc/datasheet/pinephone/PinePhone%20QZ01%20Battery%20Specification.pdf) is meant to be compatible with Samsung part number EB-BJ700BBC / BBE / CBE from the 2015 J7 phone. The extended life aftermarket BBU does fit, although it is a tight fit.

{{< admonition type="warning" >}}
 Using an aftermarket battery with a higher capacity is done at own risk. Batteries with a higher capacity especially in combination with an external charger can lead to overvoltage, which fries the modem and/or the Bluetooth and WiFi chip.
{{</ admonition >}}

The battery terminals, from the nearest to the battery edge to the nearest to the middle of battery, are as follows:

|     |     |     |     |
| --- | --- | --- | --- |
| +ve | thermistor | -ve | not connected |

The battery includes a protection circuit that isolates it in a number of fault conditions, including if it is discharged too far. The fully discharged battery can be recharged by connecting the phone to a charger with a sufficient output. Once it has charged sufficiently you will be able to boot the phone.
