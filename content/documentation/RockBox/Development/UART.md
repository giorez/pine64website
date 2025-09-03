---
title: "UART"
draft: false
menu:
  docs:
    title:
    parent: "RockBox/Development"
    identifier: "RockBox/Development/UART"
    weight: 3
---

{{< figure src="/documentation/RockBox/images/rockbox_internals.jpg" caption="Internals of the RockBox with the UART contacts visible on the bottom right" width="400" >}}

A serial console can be connected to the RockBox to retrieve the UART boot logs. A device such as a USB to TTL converter can be used to connect the RockBox. Simply set the USB device to 3.3 volts and connect GND to the GND connector on the mainboard, RTX to TX and TXD to RX. The fourth unlabelled contact on the mainboard should not be connected. 

{{< admonition type="note" >}}
 Unlike the ROCKPro64, connecting TXD does not prevent the device from booting up.
{{</ admonition >}}

Connect the USB device to the PC and use a tool such as `screen` to display the serial output:

    screen /dev/ttyUSB0 1500000

Then power up the RockBox and enjoy the serial output on the PC.

To enable UART output in the OS as well (otherwise the output would stop at "_Starting kernel ..._"), `console=ttyS2,1500000n8` can be added to the `append` line in the _/boot/extlinux.conf_ file when using _EXTLINUX_.
