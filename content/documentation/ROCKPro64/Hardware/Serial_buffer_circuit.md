---
title: "Serial buffer circuit"
draft: false
menu:
  docs:
    title:
    parent: "ROCKPro64/Hardware"
    identifier: "ROCKPro64/Hardware/Serial_buffer_circuit"
    weight:
aliases:
  - /wiki/ROCKPro64_Serial_Buffer_Circuit
---

Connecting to the ROCKPro64 single-board computer serial interface can sometimes be tricky, as the lack of buffering can cause the Uboot-SPL to stop functioning due to  transient voltage spikes during startup. This simple circuit allows a user to hot-plug their serial connection at any time, or can be left attached full time.

{{< admonition type="warning" >}}
 Please note that following these instructions comes at your own risk. While best efforts have been made to write reliable, safe instructions, the author cannot be held liable for the quality of procured components or the assembly job of the person following the instructions, and the damages caused by either of these not being up to par.
{{</ admonition >}}

## Shopping List

### Components

You may have some or all of these in your junk/parts drawer. They’re all common value, and easily recovered from scrap circuit-boards.

* **3"x4" perf board**, will be used for construction of the circuit
* **misc breakout board wires**, or any random copper wire that works, I used ribbon cable from an old floppy harness.
* **misc jumper wire with headers**, a three-pin header, and a one-pin header, since you’ll be connecting to the RP64 mainboard pin headers in different places
* **Transistors**, 1 (one) NPN-type, 2n2222 or equivalent;  and  1 (one) PNP-type, 2n2907 or equivalent
* **Resistors**, 3 (three) 4.7k&Omega; 1/4-watt;   and 2 (two)  10k&Omega; 1/4-watt
* **Serial interface jack**,  3-pin TRS audio jack works well, as does RJ45 or DB9. You only need, and use, 3 pins though.
* **Double-sided sticky tape**,  at least 1"x1", to mount the perf board to your case.

### Tools

* A soldering iron, e.g. the Pinecil
* solder, fine gauge, anything suitable for electronics
* Wire strippers, suitable for the thickness of wire you chose
* Diagonal cutters,  to trim excess leads from components and wires

## Assembly

* Start by creating "vias" using a stretch of bare wire for both ground and +3.3v along the long edges of the perf board; ground on one side, +3.3v on the opposite
* At one end of the perf board, start laying out the parts for the NPN transistor portion of the circuit, then solder down.
* At the opposite end, lay out the PNP transistor portion, and solder down.
* Connect up the serial interface jack, using enough wire to reach your desired mounting point on your case, from the mounting place for this board
* Solder the jumper wires to the perf board for the serial jack
* Solder the header jumpers to the perf board, making sure they’re long enough to reach the RP64 headers with a bit of slack.
* Let cool, affix the double-sided tape, and mount to your case.

## Install

* Mount your serial port
  * Serial RX <-> DCE RX (in)
  * Serial TX <-> DCE TX (out)
* attach the header jumpers to their respectively labeled points on the various headers
  * RP64 Ground  <->  pi2bus-6
  * RP64 RX (in) <-> pi2bus-8
  * RP64 TX (out) <-> pi2bus-10
  * RP64 3.3v <-> pi2bus-1

## Circuit

{{< figure src="/documentation/images/RockPro64-serial-buffer.png" >}}
