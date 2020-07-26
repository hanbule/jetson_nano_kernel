# 概要
jetson-nanoのカーネルソースコードに修正を加えています

# HDMI MIPIデバイスドライバの登録
https://developer.ridgerun.com/wiki/index.php?title=Toshiba_TC358743_Linux_driver_for_Jetson_TX1/TX2/Nano#Enable_driver
https://gist.github.com/nyacg/becd94a029355825a05f633f38a25b46

## Apply EDID data to TC358743 device
1080edid.txt
```
00ffffffffffff005262888800888888
1c150103800000780aEE91A3544C9926
0F505400000001010101010101010101
010101010101011d007251d01e206e28
5500c48e2100001e8c0ad08a20e02d10
103e9600138e2100001e000000fc0054
6f73686962612d4832430a20000000FD
003b3d0f2e0f1e0a2020202020200100
020321434e041303021211012021a23c
3d3e1f2309070766030c00300080E300
7F8c0ad08a20e02d10103e9600c48e21
0000188c0ad08a20e02d10103e960013
8e210000188c0aa01451f01600267c43
00138e21000098000000000000000000
00000000000000000000000000000000
00000000000000000000000000000000
```

v4l2-ctl --set-edid=file=1080edid.txt --fix-edid-checksum
v4l2-ctl --query-dv-timings
gst-launch-1.0 nvv4l2camerasrc device=/dev/video0 ! 'video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, interlace-mode=progressive, framerate=(fraction)30/1' ! nvvidconv ! 'video/x-raw(memory:NVMM), format=(string)NV12' ! nv3dsink -e


insert HDMI cable to MIPI  device !

if you want to get current LCD display's edid , you may do command "xrandr --props"
