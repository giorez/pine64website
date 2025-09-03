---
title: "Thermal tweaks"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone/Software_tricks"
    identifier: "PinePhone/Software_tricks/Thermal_tweaks"
    weight:
aliases:
  - /wiki/PinePhone_Thermal_Tweaks
---

This page explains how to read the thermal sensor data, and how to read and change the default settings.

## Under Linux

{{< admonition type="warning" >}}
 Setting wrong values for the thermal trip points poses a risk. These instructions are directed towards expert-level users and developers.
{{</ admonition >}}

Thermal management of the PinePhone CPU is handled by the thermal framework of the Linux kernel. Depending on the Linux distribution used on a PinePhone, the default settings may differ. It may be advised to lower the settings (i.e. the thermal trip point temperatures) to prevent the phone components from being damaged by excessive heat.

Current CPU temperature can be displayed using the following command:

    cat /sys/class/thermal/thermal_zone0/temp

The unit for all numeric values is millidegree Celsius. To read the thermal trip point types and current trip point temperatures, use the following:

    grep . /sys/class/thermal/thermal_zone0/trip_point_*_temp
    grep . /sys/class/thermal/thermal_zone0/trip_point_*_type

The default trip point temperatures are also available in the [A64 device tree](https://elixir.bootlin.com/linux/v5.12/source/arch/arm64/boot/dts/allwinner/sun50i-a64.dtsi#L194). The possible names and associated meanings for the trip point types are the following:

* "active"&nbsp;&ndash; a trip point to enable active cooling
* "passive"&nbsp;&ndash; a trip point to enable passive cooling
* "hot"&nbsp;&ndash; a trip point to notify emergency
* "critical"&nbsp;&ndash; hardware not reliable

The values for the trip point temperatures can be lowered individually, but make sure the trip points have the correct value for their corresponding trip type, e.g. **don’t** simply swap the values for the first and the second trip point. **Make sure not to set values higher than 110000** (i.e. 110 degrees Celsius, which is the default value) for the third threshold, as it may cause damage to the phone. Use the following commands:

    echo 55000  > /sys/class/thermal/thermal_zone0/trip_point_0_temp  # passive
    echo 75000  > /sys/class/thermal/thermal_zone0/trip_point_1_temp  # hot
    echo 100000 > /sys/class/thermal/thermal_zone0/trip_point_2_temp  # critical

Further information can be found in these documents from the Linux kenel source:

* [Documentation/thermal/sysfs-api.txt](https://www.kernel.org/doc/Documentation/thermal/sysfs-api.txt)
* [Documentation/hwmon/sysfs-interface](https://www.kernel.org/doc/Documentation/hwmon/sysfs-interface)
* [Documentation/devicetree/bindings/thermal/thermal.txt](https://www.kernel.org/doc/Documentation/devicetree/bindings/thermal/thermal.txt)
