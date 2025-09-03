---
title: "USB adapter"
draft: false
menu:
  docs:
    title:
    parent: "Pinedio"
    identifier: "Pinedio/USB_adapter"
    weight: 2
---

{{< figure src="/documentation/images/Pine64-lora-usb-adapter.jpg" caption="The PINE64 USB LoRa adapter" >}}

The PINE64 USB LoRa adapter is based on the Semtech SX1262 LoRa module and the CH341 USB bus converter chip. The **CH341** chip can be configured in multiple mode to convert USB to various serial and parallel ports. In this case, it’s configured in **synchronous serial mode**, which allows this chip to convert from USB to the SPI bus needed to talk to the SX1262 LoRa module:

```
 --------            --------------------------
 |      |            |   USB LoRa Adapter     |
 | PC   |  <--USB--> | CH341 <--SPI--> SX1262 |
 |      |            |       <--I/O-->        |
 --------            --------------------------
```

## Pins

{{< figure src="/documentation/images/Lora-usb-pins.jpg" caption="Pinout" >}}

| SX1262 Pin | Name | Description |
| --- | --- | --- |
| 1 | ANT | Antenna |
| 2 | GND2 |  |
| 3 | VREG |  |
| 4 | DCC |  |
| 5 | VCC |  |
| 6 | DIO1 | Connected on CH341 Pin 7 |
| 7 | DIO2 | Connected on CH341 Pin6 |
| 8 | DIO3 | Connected on CH341 Pin 5 |
| 9 | GND |  |
| 10 | MISO | SPI MISO (CH341 Pin 20) |
| 11 | MOSI | SPI MOSI (CH341 Pin 22) |
| 12 | SCK | SPI clock (CH341 Pin 24) |
| 13 | NSS | SPI Chip select |
| 14 | POR | Reset pin |
| 15 | Busy | Busy pin |
| 16 | GND |  |

### Kernel module for CH341

We need a driver for the CH341 USB bus converter chip. This driver will allow us to send command to the CH341 (SPI messages and access to the GPIOs). I’ve successfully build and run [this driver from **rogerjames99**](https://github.com/rogerjames99/spi-ch341-usb) on my desktop computer (running Manjaro Linux) and on my Pinebook Pro (ARM64, running Manjaro ARM Linux). For any kernel newer than 3.10 but mandatory for kernels newer than 5.15 you need to use the [dimich-dmb fork of the the **spi-ch341-usb driver.**](https://github.com/dimich-dmb/spi-ch341-usb) This fork has updated documentation for the newer kernel interfaces. If this driver gives you problems please drop by any of the social platforms in the Pine64 LoRa chat and give a holler, and if you are using a 5.15 or older kernel you can use the rogerjames99 fork.

```console
$ git clone https://github.com/rogerjames99/spi-ch341-usb.git
```
or
 $ git clone https://github.com/dimich-dmb/spi-ch341-usb.git
then
 $ cd spi-ch341-usb
 $ make
 $ sudo make install

Once the driver is installed, unload the module _ch341_ if it has been automatically loaded:

```console
$ lsmod |grep ch341
$ sudo rmmod ch341
```

On my setup, _ch341_ would be automatically loaded once I connected my USB adapter. This module drives the CH341 is asynchronous serial mode, which will not work for a SPI bus.

Then load the new module:

```console
$ sudo modprobe spi-ch341-usb
```

Plug your USB adapter and check that the module is correctly loaded :

```console
$ dmesg
[20141.872107] usb 1-1.1: USB disconnect, device number 4
[20143.820756] usb 1-1.1: new full-speed USB device number 5 using ehci-platform
[20143.973366] usb 1-1.1: New USB device found, idVendor=1a86, idProduct=5512, bcdDevice= 3.04
[20143.973413] usb 1-1.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
[20143.973434] usb 1-1.1: Product: USB UART-LPT
[20143.975137] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe: connect device
[20143.975164] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe: bNumEndpoints=3
[20143.975183] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe:   endpoint=0 type=2 dir=1 addr=2
[20143.975206] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe:   endpoint=1 type=2 dir=0 addr=2
[20143.975229] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe:   endpoint=2 type=3 dir=1 addr=1
[20143.975254] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs0 SPI slave with cs=0
[20143.975273] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs0 gpio=0 irq=0
[20143.975295] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs1 SPI slave with cs=1
[20143.975313] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs1 gpio=1 irq=1
[20143.975334] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs2 SPI slave with cs=2
[20143.975352] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output cs2 gpio=2 irq=2
[20143.975373] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  gpio4 gpio=3 irq=3
[20143.975394] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  gpio6 gpio=4 irq=4
[20143.975415] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  err gpio=5 irq=5
[20143.975435] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  pemp gpio=6 irq=6
[20143.975456] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  int gpio=7 irq=7 (hwirq)
[20143.975478] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  slct gpio=8 irq=8
[20143.975499] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  wait gpio=9 irq=9
[20143.975520] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  autofd gpio=10 irq=10
[20143.975542] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: input  addr gpio=11 irq=11
[20143.975564] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output ini gpio=12 irq=12
[20143.975585] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output write gpio=13 irq=13
[20143.975607] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output scl gpio=14 irq=14
[20143.975628] spi-ch341-usb 1-1.1:1.0: ch341_cfg_probe: output sda gpio=15 irq=15
[20143.975650] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: start
[20143.975677] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: SPI master connected to SPI bus 1
[20143.977831] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: SPI device /dev/spidev1.0 created
[20143.978183] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: SPI device /dev/spidev1.1 created
[20143.978552] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: SPI device /dev/spidev1.2 created
[20143.978726] spi-ch341-usb 1-1.1:1.0: ch341_spi_probe: done
[20143.978735] spi-ch341-usb 1-1.1:1.0: ch341_irq_probe: start
[20143.979133] spi-ch341-usb 1-1.1:1.0: ch341_irq_probe: irq_base=103
[20143.979154] spi-ch341-usb 1-1.1:1.0: ch341_irq_probe: done
[20143.979162] spi-ch341-usb 1-1.1:1.0: ch341_gpio_probe: start
[20143.979220] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=cs0 dir=0
[20143.979229] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=cs1 dir=0
[20143.979237] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=cs2 dir=0
[20143.979245] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=gpio4 dir=1
[20143.979253] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=gpio6 dir=1
[20143.979260] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=err dir=1
[20143.979268] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=pemp dir=1
[20143.979275] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=int dir=1
[20143.979283] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=slct dir=1
[20143.979290] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=wait dir=1
[20143.979298] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=autofd dir=1
[20143.979306] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=addr dir=1
[20143.979314] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=ini dir=0
[20143.979321] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=write dir=0
[20143.979329] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=scl dir=0
[20143.979337] spi-ch341-usb 1-1.1:1.0: ch341_gpio_get_direction: gpio=sda dir=0
[20143.979831] spi-ch341-usb 1-1.1:1.0: ch341_gpio_probe: registered GPIOs from 496 to 511
[20143.981152] spi-ch341-usb 1-1.1:1.0: ch341_gpio_probe: done
[20143.981212] spi-ch341-usb 1-1.1:1.0: ch341_gpio_poll_function: start
[20143.981291] spi-ch341-usb 1-1.1:1.0: ch341_usb_probe: connected
[20144.756250] usbcore: registered new interface driver ch341
[20144.756334] usbserial: USB Serial support registered for ch341-uart
```

With kernel 5.16 and newer the output is shorter:

```console
$ dmesg
[ 6744.813564] usb 1-2.1.1: new full-speed USB device number 21 using xhci_hcd
[ 6744.904377] usb 1-2.1.1: New USB device found, idVendor=1a86, idProduct=5512, bcdDevice= 3.04
[ 6744.904383] usb 1-2.1.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
[ 6744.904385] usb 1-2.1.1: Product: USB UART-LPT
[ 6744.960243] spi-ch341-usb 1-2.1.1:1.0: ch341_cfg_probe: output cs0 SPI slave with cs=0
[ 6744.960246] spi-ch341-usb 1-2.1.1:1.0: ch341_cfg_probe: output cs1 SPI slave with cs=1
[ 6744.960247] spi-ch341-usb 1-2.1.1:1.0: ch341_cfg_probe: output cs2 SPI slave with cs=2
[ 6744.960249] spi-ch341-usb 1-2.1.1:1.0: ch341_cfg_probe: input  gpio4 gpio=0 irq=0 (hwirq)
[ 6744.960251] spi-ch341-usb 1-2.1.1:1.0: ch341_cfg_probe: input  gpio5 gpio=1 irq=1
[ 6744.960302] spi-ch341-usb 1-2.1.1:1.0: ch341_spi_probe: SPI master connected to SPI bus 0
[ 6744.960350] spi-ch341-usb 1-2.1.1:1.0: ch341_spi_probe: SPI device /dev/spidev0.0 created
[ 6744.960398] spi-ch341-usb 1-2.1.1:1.0: ch341_spi_probe: SPI device /dev/spidev0.1 created
[ 6744.960445] spi-ch341-usb 1-2.1.1:1.0: ch341_spi_probe: SPI device /dev/spidev0.2 created
[ 6744.960583] spi-ch341-usb 1-2.1.1:1.0: ch341_usb_probe: connected
```

### Driver development

#### Kernels 5.14 and older

Once the module _spi-ch341-usb_ is correctly loaded, here’s how you can transfer data on the SPI bus (in C):

    /* Open the SPI bus */
    int spi = open("/dev/spidev1.0", O_RDWR);
    uint8_t mmode = SPI_MODE_0;
    uint8_t lsb = 0;
    ioctl(spi, SPI_IOC_WR_MODE, &mmode);
    ioctl(spi, SPI_IOC_WR_LSB_FIRST, &lsb);

    /* Transfer data */
    /* TODO: Init buffer_out, buffer_in and size */
    const uint8_t *mosi = buffer_out; // output data
    uint8_t *miso = buffer_in; // input data

    struct spi_ioc_transfer spi_trans;
    memset(&spi_trans, 0, sizeof(spi_trans));

    spi_trans.tx_buf = (unsigned long) mosi;
    spi_trans.rx_buf = (unsigned long) miso;
    spi_trans.cs_change = true;
    spi_trans.len = size;

    int status = ioctl (spi, SPI_IOC_MESSAGE(1), &spi_trans);

To access GPIOs, you first need to export them (to make them accessible via _/sys/class/gpio_. As you can see in the dmesg output, GPIOs from 496 to 511 were registered, which means we can export 16 GPIOs. The mapping of these I/O is available in the [source code of the driver](https://github.com/rogerjames99/spi-ch341-usb/blob/master/spi-ch341-usb.c#L148). For example, pin _slct_ is the 12th, meaning we need to export GPIO 496+12 = 508.

    int  fd;
    if ((fd = open("/sys/class/gpio/export", O_WRONLY)) == -1)   {
      perror("open ini");
      exit(-1);
    }

    if (write(fd, "508", 3) == -1){
      perror ("write export 508");
    }

Once exported, the GPIO is available in _/sys/class/gpio/sclt_ (the naming is specified by the driver). You can read the pin in C:

    int  fd;
    if ((fd = open("/sys/class/gpio/slct/value", O_RDWR)) == -1)   {
      perror("open");
    }

    char buf;
    if (read(fd, &buf, 1) == -1) {
       perror("read");
    }

    int value = (buf == '0') ? 0 : 1;

You can also write it:

    int  fd;
    if ((fd = open("/sys/class/gpio/ini/value", O_RDWR)) == -1)   {
      perror("open ini");
    }

    if (write(fd, value ? "1" : "0", 1) == -1) {
       perror ("write");
    }

#### Kernel 5.15 and newer

We need some help documenting how these interfaces work|

The driver creates these interfaces:

| Pin | SPI Function | GPIO function | GPIO name | IRQ |
| --- | --- | --- | --- | --- |
| 15 | CS0 | - | - | - |
| 16 | CS1 | - | - | - |
| 17 | CS2 | - | - | - |
| 19 | - | Input | gpio4 | hardware |
| 21 | - | Input | gpio5 | software |

The dimich-dmb fork of spi-ch341-usb works with 5.15+ kernels, but as you can see above it is not configured for the needs of the Pinedio-USB by default. I have started a branch in my fork to work on getting the driver pre-configured for our needs. The branch can be [found here.](https://github.com/UncleGrumpy/spi-ch341-usb/tree/pinedio) Please feel free to help|And open issues or discussions in the repo if you have problems or ideas how to help. Any improvements to the actual code beyond configuration should be pushed to the temporary [upstream.](https://github.com/dimich-dmb/spi-ch341-usb/)

Since linux-5.15 binding to spidev driver is required to make slave devices available via /dev/, e.g. for slave 1 on bus 0 as real root (not with sudo):

```console
# echo spidev > /sys/class/spi_master/spi0/spi0.1/driver_override
# echo spi0.1 > /sys/bus/spi/drivers/spidev/bind
```

For all devices handled by spi_ch341_usb driver (again, only as real root):

```console
# for i in /sys/bus/usb/drivers/spi-ch341-usb/*/spi_master/spi*/spi*.*; do echo spidev > $i/driver_override; echo $(basename $i) > /sys/bus/spi/drivers/spidev/bind; done
```

The documentation found at https://github.com/dimich-dmb/spi-ch341-usb/blob/master/README.md has more information.

The 5.15+ driver is not ready yet. But if you are interested in testing, helping to get the configuration right, or working on application development you can build and test the current driver:

```console
$ git clone -b pinedio https://github.com/UncleGrumpy/spi-ch341-usb.git
$ cd spi-ch341-usb
$ make
$ sudo make install
```

So far this will automatically set up the SPI slave device /dev/spi0.0. It names the ch341-usb device as "pinedio" this will allow application developers to find the correct gpiochip by name. I need help confirming the correct gpio pins but as of now the driver will setup the following configuration:

The driver uses following CH341A pins for the SPI interface.

| Pin | Name | Direction | Function SPI (CH341A) |
| --- | --- | --- | --- |
| 18 | D3 | output | SCK (DCK)           |
| 20 | D5 | output | MOSI (DOUT)         |
| 22 | D7 | input | MISO (DIN)          |
| 15 | D0 | output | CS0                 |

The driver uses the following GPIO configuration.

{{< admonition type="warning" >}}
 It is not sure if these are the correct pins to use|
{{</ admonition >}}

| CH341 Pin | CH341A Name | Function | GPIO Name | GPIO Configuration | SX1262 connection |
| --- | --- | --- | --- | --- | --- |
| 7 | INT# | IRQ | dio_irq | Input | DIO1 (IRQ)      |
| 8 | SLCT | BUSY | dio_busy | Input | BUSY            |
| 26 | RST# | Hard Reset | dio_reset | Output | NRESET          |

The function of these pins can be changed from user space by using libgpiod. The command line tools installed with the library (gpioset, gpioget, gpiodetect, gpioinfo and others can be used for bash scripts, etc. and applications should all use the libgpiod interfaces. The /sys/class/gpio interface has been removed from the kernel in 5.15, so any apps using /sys/class/gpio to access gpio pins are broken, or will be as distos update their kernels to 5.15 and beyond.

GPIO pins can be listed with gpioinfo:

```console
$ gpioinfo pinedio
```

The output should look similar to:

    gpiochip1 - 3 lines:
            line   0:    "dio_irq"       unused   input  active-high
            line   1:   "dio_busy"       unused   input  active-high
            line   2:  "dio_reset"       unused  output  active-high

The gpiochip# might be different. The driver exposes the Pinedio with the gpio name "pinedio", developers should use this name to interact with the gpiochip because the gpiochip# of the device is likely to be different from one system to the next, or depending on the order devices are initialized.

### Driver for the SX1262 LoRa module

Now that we can talk to the SX1262 via the CH341 USB converter chip, we need to send actual commands to make it emit or receive LoRa messages. To do this, you can implement the driver yourself using info from the datasheet, or use an existing driver (you can easily find drivers for the Arduino framework, for example.
I found [this C++ driver](https://github.com/YukiWorkshop/sx126x_driver). It’s well written, lightweight and easily portable across many platforms. All you have to do is implement 3 HAL function : read GPIO, write GPIO and transfer data on SPI. I wrote a quick’n’dirty app that emits a LoRa frame. It’s [available here](https://gist.github.com/JF002/f1af5595874942427eea9d375c18fc73).

As I don’t have any 'raw' LoRa device on hands, I check that it was actually transmitting something using my SDR setup (simple TNT usb key and **Gqrx** software):

{{< figure src="/documentation/images/pine64-lora-usb-adapter-sdr.png" width="500" >}}
