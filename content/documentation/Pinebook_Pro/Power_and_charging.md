---
title: "Power and charging"
draft: false
menu:
  docs:
    title:
    parent: "Pinebook_Pro"
    identifier: "Pinebook_Pro/Power_and_charging"
    weight: 4
aliases:
  - /wiki/Pinebook_Pro_power_and_charging
---

The Pinebook Pro external power and charging circuity is quite rudimentary, and hence quirky. This article aims to explain all the fine points so that the behavior could be understood and dealt with.

## Monitoring and control
### Overview

No control of charging is possible other than by physically plugging and unplugging a charger.

Software monitoring is also quite limited, one can check whether a charger is connected (in `/sys/class/power_supply/dc-charger/online` and `/sys/class/power_supply/tcpm-source-psy-4-0022/online`) and see the current battery voltage (in `/sys/class/power_supply/cw2015-battery/voltage_now`).

The [CW2015](https://cdn.datasheetspdf.com/pdf-down/C/W/2/CW2015-Cellwise.pdf) battery monitoring IC only measures the voltage and tries to estimate the State Of Charge and Remaining Run Time. The last value (along with the ''nominal'' battery capacity) is also used by the kernel driver to ''compute'' the current. The estimations might be relatively accurate under certain conditions but you can not really know if they’re met with your laptop load at any given moment, so the only value provided that can be trusted is the voltage.

### Charging indicator LED

There is a red LED near the barrel socket that’s connected directly to the [BQ24171](https://www.ti.com/lit/ds/symlink/bq24171.pdf?ts=1607068456825&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FBQ24171) battery charging IC.

It can indicate one of the three states:

1. LED ''on'' means the charger is supplying current to the battery and the system;
2. LED ''off'' means the charger is turned off, and the whole system is powered from the battery;
3. LED ''blinking with 0.5&nbsp;Hz frequency'' signals some hardware error: typically battery over-temperature protection or input under-voltage (from a failed charger); in this case the charger is also off, and the system is powered from the battery all the time.

All other kinds of blinking really indicate the charger getting turned on and off, this happens when BQ24171 detects ''battery full'' condition, disables the charger, the system starts drawing current from the battery, the voltage quickly drops, and the charger is enabled again to compensate for the discharge. The blinking frequency would depend on the current system load, battery temperature, and the backlight level (as the backlight power source adds up to ~70&nbsp;mV ripple to the voltage monitoring net). This "trickle-charging" is harmful for lithium batteries, but no workaround is possible other than fully disconnecting the external power source, and it’s not clear whether that would do more good than harm.

Another observed behavior is that the status LED blinks randomly, from time to time and unrelated to the system load, especially when the screen brightness is cranked to the maximum, and the battery isn’t fully charged.  This has been attributed to some strange feedback that the BQ24171 receives and becomes confused, but further analysis is required.

### Monitoring currents

The charging IC uses two measurement shunt resistors: ''R37'' for input current, and ''R43'' for battery current, both 0.010&nbsp;Ohm. They’re easily accessible for external equipment after removing the RF shield on the mainboard, and one can use a battery-powered voltmeter or a differential probe to properly measure the real current at any given moment. Do ''not'' connect non-isolated oscilloscope ground clip to them, that might damage the equipment.

With the external chargers disconnected the system is powered by the battery, so measuring voltage on ''R43'' (along with the battery voltage at about the same moment) can be used to learn the system power consumption under different software loads.

## Charging

### Overview

{{< figure src="/documentation/Pinebook_Pro/images/Pbp-charging-simplified.png" caption="Pinebook Pro simplified charging schematics" width="300" >}}

When an external charger is connected, the battery charging process is automatically activated, it doesn’t depend on any software interactions and works all the same even with the main SoC powered down. The system automatically chooses between the barrel socket (limiting current draw to 3&nbsp;A) and Type-C source (limited to 2.5&nbsp;A), with the former preferred when both are connected at the same time (but the current limit is enforced as if Type-C was used).

The maximum charging current under normal conditions is limited to 2.75&nbsp;A and the voltage to 4.35&nbsp;V. Battery temperature affects these values, and if the measuring is done properly (see the section [Battery temperature fix](#battery_temperature_fix)) the charge is fully suspended under 0&nbsp;°C or above 60&nbsp;°C, maximum current halved below 10&nbsp;°C, maximum voltage reduced to 4.24&nbsp;V above 45&nbsp;°C and to 4.19&nbsp;V above 50&nbsp;°C.

The charging process automatically terminates when the voltage reaches the recharge threshold (upper limit - 0.1&nbsp;V) ''and'' the current falls below 275&nbsp;mA. However, this also stops supplying external power to the system, so if it’s running the battery voltage almost immediately drops below the recharge threshold, and the charging is turned on again.

### Example run and charge time calculations

Assuming a fully charged 9600&nbsp;mAh battery and an idle system using ''performance'' cpufreq governor with backlight at 3700/4095  consuming 9.6&nbsp;W we can expect

```
9.6 Ah * 3.8 V / 9.6 W = 3.8 h
```

so that gives 3.8 hours of run time.

If the same battery is empty and a barrel plug charger is connected while system has the same load it will need

```
9.6 Ah * 3.8 V / ((3 A * 5 V * 0.9 - 9.6 W) * 0.95) = 9.85 h
```

that is 9.85 hours of charging from zero to full, assuming 0.9 DC-DC conversion efficacy and 0.95 charging efficacy.

Removing the system load reduces the time to

```
9.6 Ah * 3.8 V / (2.75 A * 3.8 V * 0.95) = 3.67 h
```

so if you need to fully charge the battery, e.g. before a trip, the fastest and most reliable way is to power down (not suspend) the system, leave the device with the charger connected for a few hours, upside down for better cooling, and wait for the red LED on the side to turn off.

### Working without battery

With the battery disconnected the charger isn’t going to turn on, and the system won’t be getting any power from the external source. That’s why PBP has additional bypass cable that allows connecting external power directly to the system power bus. Of course it should be kept disconnected when the battery is present to avoid excess voltage overcharging and destroying the battery. It’s also recommended to add additional insulation to the cable connectors, as they expose battery and charger positive terminals on bare metal, and should never be accidentally connected to ground. 

## Hardware modifications

### Type-C current limit

{{< admonition type="warning" >}}
 The 0.5&nbsp;A difference described in this section is there to carve out some power for a USB-C dock connected to the Pinebook Pro’s USB-C port.  This is actually against the USB Power Delivery specification, but it leaves some power to the USB-C dock, which it requires to power itself and any devices connected to it.  Thus, the procedure described in this section will most probably make using USB-C docks unreliable or even impossible, leaving the USB-C port usable for connecting only USB-C chargers or bus-powered USB-C devices.
{{</ admonition >}}

Since there’s no software control over the input current limit unmodified PBP always tries to draw up to 2.5&nbsp;A from a Type-C charger.

It’s recommended to manually check `/sys/class/power_supply/tcpm-source-psy-4-0022/current_max` for all the chargers you’re using. When the value is lower than 2.5&nbsp;A you shouldn’t use that charger with PBP as it would get overloaded, running out of specs.

If all of the chargers you want to use can supply 3&nbsp;A or more ''at 5&nbsp;V'' (the sysfs file will still report 2.5&nbsp;A so check the official charger specs and/or label) consider lifting the limit to make it even with the barrel plug charger. For that remove the ''R148'' resistor on the [bottom layer](https://wiki.pine64.org/images/b/b7/Pinebookpro-v2.1-bottom-ref.pdf) of the mainboard.

The easiest way is to use a soldering iron tip big enough to hold a 1&nbsp;mm drop of an SnPb solder (it mixes with Pb-free nicely and lowers the melting point) to heat both sides of the resistor at once and lift it off.

### Battery temperature fix

{{< admonition type="warning" >}}
 The procedure described in this section alters the operating parameters of the lithium battery built into the Pinebokk Pro, which may be unsafe, and in extreme conditions may even introduce a fire hazard.  Use the described procedure at your own risk.  Additional verfication of the described procedure is currently pending.
{{</ admonition >}}

To ensure safe operation the charger IC is constantly monitoring the battery temperature with the sensor integrated inside the pack. The thermistor used is a 103AT NTC but the corresponding circuity on PBP mainboard was calculated for some other type. This results in the charger IC detecting 45&nbsp;°C when the battery is in fact at just 35&nbsp;°C, and 60&nbsp;°C when the battery is at 46&nbsp;°C. It’s easy to hit this threshold with heavy CPU or GPU loads as the metal back cover heats up from the SoC and slightly warms up the battery. Under these conditions the charging is suspended (with charging LED signalling a hardware issue), and the intensive tasks are continued on battery power alone, heating it up even more.

To fix this issue the resistor divider needs to be replaced to match the datasheet recommended values. For that one needs to change two 0402 resistors on the bottom side of the mainboard: use 2.2&nbsp;kOhm 1&nbsp;% for ''R52'' (instead of 4.4&nbsp;kOhm installed by the factory), note it’s the one closer to the board edge; and 6.8&nbsp;kOhm 1&nbsp;% for ''R54'' (30&nbsp;kOhm from the factory).

If your local hackspace doesn’t have suitable resistors consider getting a sample book from e.g. Aliexpress, it should cost less than 15&nbsp;USD including shipping.
