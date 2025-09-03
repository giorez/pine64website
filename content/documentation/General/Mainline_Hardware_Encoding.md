---
title: "Mainline Hardware Encoding"
draft: false
menu:
  docs:
    title:
    parent: "General"
    identifier: "General/Mainline_Hardware_Encoding"
    weight:
aliases:
  - /wiki/Mainline_Hardware_Encoding
---

**Mainline Hardware Encoding** of video can be achieved through the V4L2 user-space API, for which currently only GStreamer implements the required code.

## SoC Support

The following table shows the current supported codecs for encoding for each SoC. Support for decoding is separate.

| | RK3328 | RK3399 | RK3566 | RK3588 |
| -------- | ------- | ------- | ------- | ------- |
| JPEG | N/A | Yes | Yes | No
| VP8 | N/A | [In review](https://lore.kernel.org/linux-rockchip/20230309125651.23911-1-andrzej.p@collabora.com/T/) | No | No
| H.264/AVC | No | No | No | No
| H.265/HEVC | No | N/A | No | No

## Encoding With GStreamer

With GStreamer, in general, any V4L2 control can be set using the `extra-controls=foo,name=value` syntax after the encode pipeline stage identifier, where `foo` is any name you wish which GStreamer will promptly ignore, `name` is the name of the V4L2 control as shown by `v4l2-ctl --list-ctrls` (make sure to pick the right device with `-d`), and `value` is whatever value you want to set it to.

### JPEG Encoding

This example converts an input MP4 file to an output MJPEG-inside-MKV file at JPEG quality 95, without any audio.

```
gst-launch-1.0 filesrc location=input.mp4 ! qtdemux name=demux demux.video_0 ! decodebin ! videoconvert ! v4l2jpegenc extra-controls=s,compression_quality=95 ! matroskamux ! filesink location=output.mkv
```

### VP8 Encoding

{{< admonition type="tip" >}}
This requires a draft [GStreamer merge request](https://gitlab.freedesktop.org/gstreamer/gstreamer/-/merge_requests/3736) and the RFC kernel patchset applied.
{{</ admonition >}}

This example converts an input MP4 file to an output VP8-inside-MKV file with a quantiser between 12 and 28, without any audio. The quantiser value goes from 0 (best quality, biggest filesize) to 63 (worst quality, smallest filesize).

```
gst-launch-1.0 filesrc location=input.mp4 ! qtdemux name=demux demux.video_0 ! decodebin ! videoconvert ! v4l2slvp8enc min-quality=12 max-quality=28 ! queue ! matroskamux ! filesink location=output.mkv
```

Alternatively, you can encode in variable bitrate mode with a target bitrate given in bits per second. Do note that Hantro doesn’t seem to do target bitrates below 2 mbit/s. In this example, the file is transcoded at a target bitrate of 3 megabits per second.

```
gst-launch-1.0 filesrc location=input.mp4 ! qtdemux name=demux demux.video_0 ! decodebin ! videoconvert ! v4l2slvp8enc bitrate=3000000 ! queue ! matroskamux ! filesink location=output.mkv
```
