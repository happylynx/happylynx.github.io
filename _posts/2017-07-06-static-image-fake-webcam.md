---
title: Static image fake webcam
---

## Static image fake webcam

This post describes how to create a dummy webcam that will provide stream of static image.

1. Install [v4l2loopback][1].  
   Make sure version of current kernel (`uname -r`) matches the version of `kernel-devel` package.
2. Activate compiled kernel module

       sudo modprobe v4l2loopback
   
3. Provided previous step created new device `/dev/video1`, instruct `ffmpeg` to fed the video device by image data

       ffmpeg -loop 1 -re -i <path-to-the-image> -f v4l2 -vcodec rawvideo -pix_fmt yuv420p /dev/video1
       
Reference: https://github.com/umlaeute/v4l2loopback/wiki/Ffmpeg

[1]: https://github.com/umlaeute/v4l2loopback
