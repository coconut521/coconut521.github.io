---
title: Fan Control in ASUS Vivobook
createTime: 2025/05/23 08:43:42
permalink: /arch/hxwrnk6i/
tags:
    - Archlinux
    - Linux
    - ASUS
---

> When I try installing Archlinux on my ASUS Vivobook, I met problem with the ==automatic fan control==.

# Problems

After succeeded installing Archlinux, I tried to play Euro Turck Simulator 2 on my device and fund that both fans wasn't controlled automatically. They were running in a very low speed and, consequently, my computer went power off directly due to overheated (I was not sure wether the CPU or the GPU did). 

Notably there are not any useful solutions for my device *(ASUS Vivobook K6604JV)* on [archwiki-Fan speed control](https://wiki.archlinux.org/title/Fan_speed_control), even though there is a part of instuction for ASUS devices. I had tried [asus-fan](https://wiki.archlinux.org/title/Fan_speed_control#asus_fan) but still not got automatic control of the fan. The only thing I could adjust is to change the fan speed to maximum, **which is quite stupid.**

## Device Information

| Properties    | Model         |
| :-----------: |:-------------:|
| CPU      | Intel i9-13980HX |
| Memory      | 32GB      |
| Disk | NVMe Samsung SSD 990 PRO 2TB  |
| GPU0 | Intel UHD Graphics |
| GPU1 | NVIDIA GeForce RTX 4060 Laptop GPU |

# Approaching to Solution

Then, I tried to play games by the command below.

```sh
echo 0 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1_enable      # Change GPU fan mode to full speed
echo 0 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm2_enable      # Change GFX fan mode to full speed
```

I know what you are thinking about. **THAT IS QUITE STUPID** to set the fans fully running before the game and set it back to lower speed after the entertainment, which makes the entertainment disapper at all.


:::: tip

The solution I finnaly got is installing ==asusctl==, which made me re-realized the unbelivible power of archlinux community. ==There is the [asusctl-manual](https://asus-linux.org/manual/asusctl-manual/).==

And there is the [installation guide](https://asus-linux.org/guides/arch-guide/)


```sh
pacman-key --recv-keys 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --lsign-key 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35

wget "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x8b15a6b0e9a3fa35" -O g14.sec
sudo pacman-key -a g14.sec
```

Then add:

::: code-tabs

@tab /etc/pacman.conf

```
[g14]
Server = https://arch.asus-linux.org
# https://arch.asus-linux.org # Germany, origin
# https://naru.jhyub.dev/$repo # Republic of Korea
```
:::

```sh
pacman -Syu
pacman -S asusctl power-profiles-daemon
systemctl enable --now power-profiles-daemon.service

pacman -S supergfxctl switcheroo-control
systemctl enable --now supergfxd
systemctl enable --now switcheroo-control

pacman -S rog-control-center

# Custome Kernel with Driver Support
pacman -Sy linux-g14 linux-g14-headers
grub-mkconfig -o /boot/grub/grub.cfg
```


::::
