---
title: "Hardware checking"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone_Pro/Factory_tests"
    identifier: "PinePhone_Pro/Factory_tests/Factory_test_hardware_checking"
    weight:
---

{{< figure src="/documentation/images/PPP_Abdroid_Test_Utility-5.jpg" width="400" >}}

{{< admonition type="note" >}}
Please note that this Android build solely for PinePhone Pro hardware checking purpose and solely used by the support team. This is not a general release build.
{{</ admonition >}}

Download:

* [Direct download](https://files.pine64.org/os/PinePhonePro/pinephone_pro_dd_android9_QC_Test_SDboot_20220215-8GB.img.gz) from _pine64.org_ (722MB, for 8GB microSD cards or bigger, MD5 of the GZip file _214e063c8205c1a98d44b2015a21bb5d_)

Instructions:

* Download the build, extract the image and dd it to a 8 GB or larger microSD card, take out the PinePhone Pro Explorer Edition, then insert it into microSD slot (upper slot).
* Insert battery, press the RE button (bypass SPI and eMMC boot) underneath the back cover while plugging in the USB-C power. After 3 seconds release the RE button.
* When powering up, a battery icon screen will show up. Press the power key for two seconds, then the Rockchip logo screen shows up.

{{< figure src="/documentation/images/PPP_Abdroid_Test_Utility-1.jpg" width="300" >}}

* Wait for the home screen, double tap on the test app icon (mark red circuit) and this will bring up the factory test screen. Please note that the SD test is disabled due in this is SD boot build.
* After running a particular test function, please snapshot the test result and pass it back to support team

Notes:

* Please insert a functional SIM card when performing the SIM test
* When perform GPS test, the first result may fail and please ignore this false message.
* For light sensing test, please have a light shine to the PinePhone Pro when performing the test.

{{< figure src="/documentation/images/PPP_Abdroid_Test_Utility-4.jpg" width="300" >}}
