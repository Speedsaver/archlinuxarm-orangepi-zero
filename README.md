This repository can be used to create an ArchLinuxARM image for the OrangePi
Zero board. This is a fork and has been updated to use more recent u-boot and kernel since the 4.13 kernel isn't required anymore.

Dependencies
============
```
sudo apt install autoconf bison fdisk flex gawk gcc-arm-none-eabi help2man libarchive-tools libtool libtool-bin make sudo swig texinfo
```
Preparing the files
===================
```
git clone https://github.com/Speedsaver/archlinuxarm-orangepi-zero.git
```
```
cd archlinuxarm-orangepi-zero
```
```
make
```


This will provide:

- the ArchLinuxARM armv7 default rootfs (`ArchLinuxARM-armv7-latest.tar.gz`)
- an u-boot image compiled for the OrangePi Zero (`u-boot-sunxi-with-spl.bin`)
- a boot script (`boot.scr`) to be copied in `/boot`


Installing the distribution
===========================

Insert a micro sd card, unmount and run `
```
make install BLOCK_DEVICE=/dev/sdx
```
with the appropriate value for
`BLOCK_DEVICE`(run lsblk to verify the value required for x after sd).

This is running commands similar to [any other AllWinner ArchLinuxARM
installation][alarm-allwinner].

[alarm-allwinner]: https://archlinuxarm.org/platforms/armv7/allwinner/.

Transfer the micro sd card to your Orange Pi Zero and power up, the green onboard boot LED should light.

DHCP and SSH are enabled by default, connect your OPi0 to your network via Ethernet cable and from a terminal on any network machine type:

```
ssh alarm@alarm
```
Type yes at the prompt, then the password is alarm

Once logged in via ssh go root by typing:

```
su
```
The password is root

Then type the following commands, in this order, to update Archlinuxarm on your Orange Pi Zero device and you'll be good to go:

```
pacman-key --init
```
```
pacman-key --populate archlinuxarm
```
```
pacman -Syu
```

ENJOY!!

Goodies
=======

If you have a serial cable and `miniterm.py` installed (`python-pyserial`),
`make serial` will open a session with the appropriate settings.
