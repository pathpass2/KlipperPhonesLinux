`/etc/X11/xorg.conf.d/00-rotate.conf`            
```
Section "InputClass"
       Identifier "libinput touchscreen catchall"
       Option "CalibrationMatrix" "0 1 0 -1 0 1 0 0 1"
       MatchIsTouchscreen "on"
       MatchDevicePath "/dev/input/event*"
       Driver "libinput"
EndSection

Section "Device"
    Identifier "FBDEV"
    Driver "fbdev"           # 强制使用 fbdev 驱动
    Option "Rotate" "CW"     # CW=顺时针, CCW=逆时针, UD=180°
    Option "IgnoreACMI" "true"    # 忽略调色板错误
    Option "ShadowFB" "false"     # 禁用影子缓冲
EndSection
```

`while true; do echo 1 | sudo tee /sys/class/graphics/fb0/rotate >/dev/null; sleep 0.02; done`
