Fan-control 
==============

A tool to control 25W POE Hat fan speed by temperature automatically for ROCK5B.

Features
--------------
1. Control fan speed by temperature. (above 45 degrees)
2. set fan speed manually

Prerequisites
=============
Device Tree Overlay enabling PWM8 is required.

Enable pwm8 overlay via `armbian-config` or add manually

```bash
# fetch device tree overlay from vendor kernel
wget https://raw.githubusercontent.com/armbian/linux-rockchip/rk-6.1-rkr1/arch/arm64/boot/dts/rockchip/overlay/rk3588-pwm8-m0.dts

# compile overlay
dtc -O dtb -o rk3588-pwm8-m0.dtbo -b 0 -@ rk3588-pwm8-m0.dts

# copy and update prefix to match armbian default of `rockchip-rk3588'
cp rk3588-wm8-m0.dtbo /boot/dtb/rockchip/overlay/rockchip-rk3588-pwm8-m0.dtbo

# enable overlay in /boot/armbianEnv.txt -- assumes no other overlays exist
# you may want to do this via armbian-config now instead
echo "overlays=pwm8-m0" >> /boot/armbianEnv.txt
```
rebooo afterwards to load overlay

Build & install
==============
```shell
make package
dpkg -i fan-control*.deb
```

Usage
==============
```shell
systemctl enable fan-control
systemctl start fan-control
```
  
Configuration
==============

configuration file locations is `/etc/fan-control.json`, Configuration parameter description:

|Configuration|Description|
|--|--|
|pwmchip|pwmchip id, 1 for auto scan|
|gpio|gpio id, 0 is default gpio |
|pwm-period|PWM period|
|temp-map|temperature configuration table|
|temp|temperature, in degrees Celsius|
|duty|duty ratio|
|duration|duration, in second|


License
===============
MIT License


