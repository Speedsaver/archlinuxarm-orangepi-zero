This repository can be used to create an ArchLinuxARM image for the OrangePi
Zero board. This is a fork and has been updated to use more recent u-boot and kernel since the 4.13 kernel isn't required anymore.

Dependencies
============

- `make`
- `bsdtar` (`libarchive`)
- `uboot-tools`
- `swig`
- `sudo`
- `fdisk`

Prerequisite
============

In order to build the image, you need a working ARM toolchain.

Here is a simple way to get one: (note dependencies for Ubuntu sudo apt install u-boot-tools libarchive-tools autoconf flex texinfo help2man gawk libtool libtool-bin bison)

    git clone https://github.com/crosstool-ng/crosstool-ng
    cd crosstool-ng
    ./bootstrap
    ./configure --enable-local
    make
    ./ct-ng arm-unknown-eabi
    ./ct-ng build

If you use this method, please edit the Makefile to change the prefix of the toolchain from `arm-none-eabi-` to `arm-unknown-eabi-`.
Alternatively if you run archlinux, you can install the arm-noneabi toolchain (gcc, binutils...)
On ubuntu you can install gcc-arm-none-eabi.

Preparing the files
===================

Run `make` (specifying jobs with `-jX` is supported and recommended).

This will provide:

- the ArchLinuxARM armv7 default rootfs (`ArchLinuxARM-armv7-latest.tar.gz`)
- an u-boot image compiled for the OrangePi Zero (`u-boot-sunxi-with-spl.bin`)
- a boot script (`boot.scr`) to be copied in `/boot`


Installing the distribution
===========================

Run `make install BLOCK_DEVICE=/dev/mmcblk0` with the appropriate value for
`BLOCK_DEVICE`.

This is running commands similar to [any other AllWinner ArchLinuxARM
installation][alarm-allwinner].

[alarm-allwinner]: https://archlinuxarm.org/platforms/armv7/allwinner/.

Goodies
=======

If you have a serial cable and `miniterm.py` installed (`python-pyserial`),
`make serial` will open a session with the appropriate settings.
