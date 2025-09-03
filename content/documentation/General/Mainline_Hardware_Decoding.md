---
title: "Mainline Hardware Decoding"
draft: false
menu:
  docs:
    title:
    parent: "General"
    identifier: "General/Mainline_Hardware_Decoding"
    weight:
aliases:
  - /wiki/Mainline_Hardware_Decoding
  - /wiki/Hardware_acceleration
---

{{< admonition type="note" >}}
This page is incomplete, you're welcome to improve it.
{{</ admonition >}}

*Mainline Hardware Decoding* refers to video decoding done using hardware accelerators on the mainline Linux kernel (i.e. what sits in Linus' tree).

On most consumer-oriented SoCs, there is what is referred to as a VPU (Video Processing Unit). The VPU is responsible for power-efficient encoding and decoding of videos. Hardware-accelerated video decoding can be useful to get smoother video playback on your devices, lower power consumption, and lower CPU utilization. Below is information regarding various hardware PINE64 uses and software that works with it.

## Hardware

Here's a table of the current support for different hardware. "In review" means the patch series to enable support has been posted to the mailing lists but is undergoing review, "linux-next" means it has been accepted and staged for the next Linux merge window.

| | RK3328 | RK3399 | RK3566 | RK3588 |
| -------- | ------- | ------- | ------- | ------- |
| JPEG | No | Yes | No | No |
| MPEG-2 | Yes | Yes | Yes | No  |
| MPEG-4 Part 2/H.263 | No | No | No | No |
| VP8 | Yes | Yes | Yes | No |
| H.264/AVC | Yes | Yes | Yes¹| No |
| H.265/HEVC | In review | In review | No | No |
| VP9 | Yes | Yes | No | No |
| AVS2 | N/A | N/A | N/A | No |
| AV1 | N/A | N/A | N/A | No |

### Notes

¹ only Hantro, not rkvdec2, so with a maximum resolution of 1080p for now

### Cedrus

In 2018, Bootlin launched a crowdfunding campaign to bring a open source Allwinner VPU driver to mainline Linux, which came to be called Cedrus. The Cedrus media driver (For Allwinner SOCs such as A64) supported by mainline Linux supports H.264 and H.265 video decoding as of Linux 5.10, and with 5.11 came VP8 decoding support and a H.264 stateless video decoder interface. For more information refer to the [Sunxi wiki](https://linux-sunxi.org/Sunxi-Cedrus#Codec_Support).

### Hantro

The Hantro media driver supports Rockchip and NXP SoCs including the RK3399 used in the Pinebook Pro and RockPro64. In November 2020 it [was announced](https://www.cnx-software.com/2020/11/24/hantro-h1-hardware-accelerated-video-encoding-support-in-mainline-linux/) that Bootlin was working on encoding support for the driver.

### rkvdec

rkvdec is the video decoding hardware that's developed by Rockchip presumably in house. It's what Rockchip uses for decoding 4K H.264/AVC, VP9 and H.265/HEVC content. The driver in mainline linux for the first generation rkvdec (used in RK3328 and RK3399) supports VP9 and H.264, [patches for HEVC support](https://patchwork.kernel.org/project/linux-rockchip/list/?series=659401) are also in the process of review.

RK3566, RK3568 and likely RK3588 use a second generation of rkvdec called rkvdec2. No mainline driver for this exists yet. The rkvdec instance on RK3588 additionally supports the [AVS2 video codec](https://en.wikipedia.org/wiki/Audio_Video_Standard).

### rkdjpeg

rkdjpeg is Rockchip's in-house hardware accelerated JPEG decoder. It can be found on the RK3566 and RK3568 as well as the RK3588.

No mainline driver exists for it so far.

## Software

### GStreamer

H.264 video decoding is possible when using GStreamer built from source, or an application utilizing it such as [Clapper](https://github.com/Rafostar/clapper) or [µPlayer](https://flathub.org/apps/details/org.sigxcpu.Livi). µPlayer includes a indicator of when hardware acceleration is properly working and in use.

### FFmpeg

Mainline FFmpeg currently lacks the necessary patches to use the v4l2-requests based API, but [a fork that can utilize it exists](https://github.com/jernejsk/FFmpeg).

With the patched ffmpeg, you can utilize hardware decoding using the `-hwaccel drm` parameter, e.g.:

`ffmpeg -hwaccel drm -i input.mp4 -f null - -benchmark`

to measure how fast it decodes.

### mpv

mpv v0.35 or later, built against the aforementioned FFmpeg fork, can be used to play back videos with hardware accelerated decoding. The hardware decoder path features interop with the GPU output, saving an expensive copyback operation. You can utilize the hardware decoding with e.g.:

`mpv --hwdec=drm [FILE]`

In mpv versions prior to 0.35, you can use the copyback hwdec with:

`mpv --hwdec=drm-copy [FILE]`

## More Resources

* [Megi's Cedrus Information](https://xnux.eu/devices/feature/cedrus-pp.html)
* [HW accelerated GStreamer playback on the PinePhone](https://briandaniels.me/2021/06/27/hardware-accelerated-video-playback-on-the-pinephone.html)
* [HW accelerated Clapper video player on the PinePhone](https://briandaniels.me/2021/07/06/hardware-accelerated-video-playback-on-the-pinephone-with-clapper.html)