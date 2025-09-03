---
title: "Getting started"
draft: false
menu:
  docs:
    title:
    parent: "PineTab2"
    identifier: "PineTab2/Getting_started"
    weight: 1
---

The PineTab2 box contains two smaller boxes.

The first box includes:

* the PineTab2, 
* a short user guide, 
* a power cable and 
* the UART adapter. Note that the UART adapter is in the same package as the power cable in a second compartment and can be a bit hidden. 

The second box has the keyboard in it.

## First start

The PineTab2 can be started by pressing and holding the power button for two seconds. The device is initialized at the first boot and will power-cycle while the partition table is populated.

{{< admonition type="info" >}}
If the initialization process is interrupted it might lead to a corrupted operating system installation. In that case reinstall the operating system as explained below.
{{</ admonition >}}

The PineTab2 ships with _DanctNix Arch Linux_ and comes with a pre-set user and the default password `123456`. 

| Default credentials | |
| -------- | ------- |
| `alarm` | `123456` |

You can create a new user and set your own password after the initial boot. To do so, go to _system settings_ -> _users_ and create a new profile using your preferred name and password.

## Keyboard cover

When connecting the keyboard to the Pinetab2 ensure that the camera and the golden pogo pin connectors are correctly aligned. 
The external keyboard has 5 connection pins (the golden pins). four are standard USB connectors and one is used to detect that the keyboard is connected.

The backlight can be changed with the key combination _Pinekey + Ctrl (right)_.
