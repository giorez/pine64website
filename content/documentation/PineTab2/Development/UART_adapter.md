---
title: "UART adapter"
draft: false
menu:
  docs:
    title:
    parent: "PineTab2/Development"
    identifier: "PineTab2/Development/UART_adapter"
    weight:
---

{{< figure src="/documentation/PineTab2/images/PineTab2_USB_UARTv2.jpg" caption="The UART adapter" width="450" >}}

The USB-C UART adapter can be connected to the PineTab2 to debug boot issues at the early boot:

* Plug the adapter face-up in the USB-C port furthest away from the power button. If all the lights are lit, you have the wrong port: only the green light should be lit when you first plug it in.
* Plug USB-C cable into the port on the adapter marked "DEBUG" (the other port can be used as a power delivery passthrough so you can charge and debug at the same time)
* Set the 'SD BOOT MASKROM' switch to OFF if no SD card is inserted and you do not plan to boot from an SD card. If the switch is set to ON without an SD card present, the tablet may fail to boot.
* Open a terminal window
* Install _minicom_ or _screen_ via your distribution’s package manager, if you don’t have it installed already
* Connect via minicom using `sudo minicom -D /dev/ttyUSB0 -b 1500000` or via screen using `sudo screen /dev/ttyUSB0 1500000`
  * Ubuntu-based distro users may encounter the error, "cannot open /dev/ttyUSB0: No such file or directory". If this occurs, check the output of `sudo dmesg --follow` and unplug/replug the USB to look for any errors. If you see an error like, "usb 1-1: usbfs: interface 0 claimed by ch341 while 'brltty' sets config #1", then the brltty service is likely conflicting with this device. Brltty provides access to blind users who use a braille display: if you do not need this service, try disabling it using these commands:
    * `sudo systemctl stop brltty-udev.service`
    * `sudo systemctl mask brltty-udev.service`
    * `sudo systemctl stop brltty.service`
    * `sudo systemctl mask brltty.service`
