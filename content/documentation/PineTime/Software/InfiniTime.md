---
title: "InfiniTime"
draft: false
menu:
  docs:
    title:
    parent: "PineTime/Software"
    identifier: "PineTime/Software/InfiniTime"
    weight:
aliases:
  - /wiki/InfiniTime
---

## InfiniTime
InfiniTime (also known as JF’s project, FreeRTOS firmware or Pinetime-JF) is an open source (GPLv3) firmware written in {cpp} and based on FreeRTOS, LVGL and NimBLE. This firmware (version 0.7.1) is preloaded at the factory since the new batch of PineTime devkits and sealed PineTimes of end of September 2020. **This page contains general information about the project. Actual project documentation and nuances are documented in the repository**

* GitHub repo: https://github.com/InfiniTimeOrg/InfiniTime
* Official website: https://infinitime.io/

## Read this first!

* InfiniTime and the bootloader are still in heavy development, and some features might not work as expected. Any issues should be reported on GitHub.
* Do not use a sealed PineTime as a development device, there is a fair amount of chances that you’ll brick it with very experimental firmware.
* OTA is relatively stable, but when you’re on an outdated bootloader version it can freeze which will require you to wait for the battery to run out.

## Known issues

{{< admonition type="warning" >}}
 Please read this section carefully before upgrading the firmware on your PineTime, especially if you are using a sealed device!
{{</ admonition >}}

### Black screen after a reset in sleep mode

#### Description
This issue occurs if you are using the original bootloader (from InfiniTime 0.7.1), upgraded from InfiniTime 0.7.1 to 0.8.2 and the watch resets while the display is OFF: the watch is stuck on a black screen and does not respond to touch, button press or BLE.

The reset can be triggered by the watchdog or manually by long pressing the button. If that doesn’t work, wait for the battery to run out, it’ll reboot then.

This issue is caused by InfiniTime 0.8.2 that put the external SPI flash memory to sleep before switching the display off and by the bootloader that cannot wake the memory chip up. The bootloader is stuck in an infinite loop.

More info: https://github.com/lupyuen/pinetime-rust-mynewt/issues/24 and https://github.com/JF002/InfiniTime/issues/60

#### Workaround

On a development kit, a simple reset via SWD is needed to unlock the bootloader.

On a sealed device, the only way to work around this issue is to wait for the battery to drain completely before trying again.

This issue can be avoided by ensuring that the display is ON when manually resetting the device (long push on the button).

#### Fixed version

This issues is fixed in [InfiniTime 0.8.3](https://github.com/JF002/InfiniTime/releases/tag/0.8.3)

## Releases

In the order of oldest first.

### Version 0.7.1

Link: [Version 0.7.1](https://github.com/JF002/InfiniTime/releases/tag/0.7.1)

This is the version that ships with PineTime devkits and sealed PineTime as of September 2020.

* Time synchronization over BLE
* Display brightness setting
* Notifications over BLE
* Integration with AmazFish (SailFishOS) and Gadgetbridge (Android)
* OTA using NRFConnect

Bootloader: https://github.com/lupyuen/pinetime-rust-mynewt/releases/tag/v4.1.7

### Version 0.8.2

Link: [Version 0.8.2](https://github.com/JF002/InfiniTime/releases/tag/0.8.2)

* Music control app
* Paint app
* Manual image validation after OTA

Bootloader: https://github.com/lupyuen/pinetime-rust-mynewt/releases/tag/v5.0.4.

This new version of the bootloader fixes [Black screen after a reset in sleep mode](#black_screen_after_a_reset_in_sleep_mode) and enables the watchdog before launching the firmware.

### Version 0.8.3

Link: [Version 0.8.3](https://github.com/JF002/InfiniTime/releases/tag/0.8.3)

* Fixes the "bootloader stuck after a reset" mentioned in 0.8.2 above

### Version 0.9.0

Link: [Version 0.9.0](https://github.com/JF002/InfiniTime/releases/tag/0.9.0)

* Touch panel fixed (no more freezing)
* Improved music application (possibility to control both volumes and browsing, display the song progression)
* Notification UI rewritten: can now display up to 100 characters
* Improved BLE connectivity

### Version 0.10.0

Link: [Version 0.10.0](https://github.com/JF002/InfiniTime/releases/tag/0.10.0)

* 2 new games: Pong and 2048
* Fixed display glitches and improved needed time to turn on the display

### Version 0.11.0

Link: [Version 0.11.0](https://github.com/JF002/InfiniTime/releases/tag/0.11.0)

* Heart-rate sensor application:
* Displays the current value, and when running, this value is also displayed on the clock face
* Value exposed over BLE, meaning other applications can read it (e.g. companion app such as Amazfish)
* Navigation app: InfiNav - works e.g. with PureMaps on SailfishOS

### Version 0.12.0

Link: [Version 0.12.0](https://github.com/JF002/InfiniTime/releases/tag/0.12.0)

* Improved BLE connection
* OTA updates much more reliable

### Version 0.13.0

Link: [Version 0.13.0](https://github.com/JF002/InfiniTime/releases/tag/0.13.0)

* Vibration
* Call notification: it is possible to accept/ignore/reject a call from the PineTime
* Music app got nicer icons
* BLE connectivity improved a bit more

### Version 0.14.0 "Green Avocado"

Link: [Version 0.14.0 "Green Avocado"](https://github.com/JF002/InfiniTime/releases/tag/0.14.0)

* LVGL 7
* Bugfixes to the build process

### Version 0.14.1

Link: [Version 0.14.1](https://github.com/JF002/InfiniTime/releases/tag/0.14.1)

* New Recovery firmware
* MCUBoot based [bootloader](https://github.com/JF002/pinetime-mcuboot-bootloader/releases/tag/1.0.0)

### Version 0.15.0 "Yellow Banana"

Link: [Version 0.15.0 "Yellow Banana"](https://github.com/JF002/InfiniTime/releases/tag/0.15.0)

* Analog watch face
* Support for switching watch faces
* Stopwatch app

### Version 1.0.0 "Red Cherry"

Link: [Version 1.0.0 "Red Cherry"](https://github.com/JF002/InfiniTime/releases/tag/1.0.0)

* Motion sensor integration
* Step countin
* UI redesign
* Quick action menu:
* Brightness setting
* Do not disturb mode (disable vibrations on notifications)
* Flash light application
* Settings menu allowing configuration of:
* Display timeout
* Wakeup source (button only, single tap, double tap and wrist rotation)
* Time format (12/24H)
* Watchface
* New navigation flow:
* User settings stored in flash memory and restored on reset

### Version 1.1.0 "Dragon Fruit"

Link: [Version 1.1.0 "Dragon Fruit"](https://github.com/JF002/InfiniTime/releases/tag/1.1.0)

* Steps application
* Timer application
* UI improvements
* Clang-format and clang-tidy config files
* Bugfixes

### Version 1.2.0 "Blue-purple Elderberry"

Link: [Version 1.2.0 "Blue-purple Elderberry"](https://github.com/JF002/InfiniTime/releases/tag/1.2.0)

* Added support for alternate accelerometer part BMA425
* Metronome app
* Memory usage optimizations
* Bugfixes, minor improvements and code cleanup

### Version 1.3.0 "Purple Fig"

Link: [Version 1.3.0 "Purple Fig"](https://github.com/JF002/InfiniTime/releases/tag/1.3.0)

* LittleFS integration
* New watchface, PineTimeStyle
* Battery level notification on BLE (supported by Gadgetbridge)
* Improved stopwatch app, Paddle game and call notifications
* Firmware update app is now more foolproof
* The SPI flash is put in sleep mode when the watch goes to sleep (only if the new bootloader is detected)
* UI improvements (better 'tick' handling in LVGL, more consistent refresh rate)
* Various improvements and code cleaning

### Version 1.4.0 "Pink Grapefruit"

Link: [Version 1.4.0 "Pink Grapefruit"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.4.0)

* Improved touch driver
* Color customization for background, text and lateral bar of PineTimeStyle
* UI improvements for better use of the small screen, and screen dimming before display sleeps
* Call notification improvements
* Battery level improvements
* Attempts to fix bootloop issue
 
### Version 1.5.0 "Huckleberry"

Link: [Version 1.5.0 "Huckleberry"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.5.0)

* Alarm app
* Vibration improvements
* Ability to recover time after a reset
* BLE improvements
* Battery level improvements
 
### Version 1.6.0 "Ice Apple"

Link: [Version 1.6.0 "Ice Apple"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.6.0)

* A new BLE Fix

### Version 1.7.0 "Jackfruit"

Link: [Version 1.7.0 "Jackfruit"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.7.0)

* More accurate battery percentage
* Faster wakeup (video)
* New touch handler
* Wake on notification and charge
* Memory usage and speed optimizations
* Motion service (video)
* Flashlight brightness changes
* Manual date and time setting
* Battery percentage reporting
* Disabled Touch Controller error check
* Paddle game bounds checking

### Version 1.7.1

Link: [Version 1.7.1](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.7.1)

* Touchscreen failure edge case

### Version 1.8.0 "Fuzzy Kiwi"

Link: [Version 1.8.0 "Fuzzy Kiwi"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.8.0)

* Improved gesture consistency
* Digital watchface: Changed the color of the BLE icon to the official "Bluetooth™ blue"
* PineTimeStyle: Integrated color picker into the watchface (long tap on the PTS watch face, and then tap on the gear icon that appears to open the color settings)    * PineTimeStyle: Fixed alignment of the icons
* Settings: Styled checkboxes as radio buttons
* Paddle: Speed randomization
* InfiniPaint: Vibration on color change (long tap to change color when running InfiniPaint)
* BLE secure pairing
* BLE file system API
* Weather service (integrations are planned for the future)
* Trip meter in Step app
* Chimes: Short vibration every hour or half an hour. Settings are available in the 3rd page of settings
* Shake to wake: The calibration of the sensitivity is available in the 3rd page of settings

### Version 1.9.0 "Limeberry"

Link: [Version 1.9.0 "Limeberry"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.9.0)

* Terminal watchface
* Enable/Disable BLE
* InfiniSim, the LVGL simulator for InfiniTime
* Improve notification and call notification timeout
* Improve heart-rate measurements
* Improve Alarm App
* Better 12-hours mode integration (in settings, alarm and status bar)
* Code cleanup and many improvements needed by InfiniSim
* Fix display corruption when the timer is triggered
* Fix freeze in Music app when the title/album name were too long

### Version 1.10.0 "Yellow Mango"

Link: [Version 1.10.0 "Yellow Mango"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.10.0)

* Notifications can now be dismissed by right swiping on the notification
* Faster sleep
* New sharper battery icon
* Timer UI was overhauled
* Tweaked and improved display gamma to improve the colors displayed by the LCD
* Flashlight now defaults to max brightness
* Fixed track progress in Music app
* Fixed alarm sometimes not ringing

### Version 1.11.0 "Red Nectarine"

Link: [Version 1.11.0 "Red Nectarine"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.11.0)

* Ability to install external resources, such as watch faces, images, and fonts.
* Created a document to better communicate the vision of InfiniTime project to users, developers and everyone else
* Compatibility with LFCLK calibration and reduced the power consumption of Nimble
* Limit backlight brightness when flashlight is off
* Watch face inspired by the G7710, with day of year and week number info (+ battery level %)
* Infineat watch face + its external resources
* Added pink color for PinetimeStyle watch face
* PineTimeStyle watch face : make step count display configurable (full gauge for step count, half gauge with seconds and numerical display of the step count).

### Oneshot 1.11 - FOSDEM 2023 Edition

Link: [Oneshot 1.11 - FOSDEM 2023 Edition](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.11.0-fosdem-edition)

* Oneshot version, which was created for the "Free and Open source Software Developers' European Meeting"
* Digital and analog watchfaces with FOSDEM’s logo as the background

### Version 1.12.0 "Olallieberry"

Link: [Version 1.12.0 "Olallieberry"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.12.0)

* Project maintenance
* Added Watchmate to the list of companion apps
* Better battery level monitoring, and battery indicator alert
* Date and time settings are combined into a single setting page
* Updated settings list style

### Version 1.13.0 "Pomegranate"

Link: [Version 1.13.0 "Pomegranate"](https://github.com/InfiniTimeOrg/InfiniTime/releases/tag/1.13.0)

* New heart rate processing algorithm, provides more accurate and faster results
* New memory management (heap unification)
* Weather integration in PineTimeStyle watch face
* Major power optimizations
* Bug fix in shake wake
