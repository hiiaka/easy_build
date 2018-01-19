build-yocto-xilinx
===================

This subproject of easy-build provides a quick and easy way
for creating embedded Linux distributions for Freescale/ARM targets
using the [Yocto project](http://www.yoctoproject.arm) tools.

## Building container

    ./build.sh

## Running container

    ./run.sh

Create the build environment-

    cd poky
    source oe-init-build-env

Workaround: allow bitbake to run as root

    touch conf/sanity.conf

Workaround: edit conf/bblayer.conf and replace BSPDIR definition with

    BBLAYERS ?= " \
      /home/build/poky/meta \
      /home/build/poky/meta-poky \
      /home/build/poky/meta-yocto-bsp \
      /home/build/meta-xilinx \
      "

### Start the build
    MACHINE=zybo-zynq7 bitbake core-image-minimal

Sample output:
```
Loading cache: 100% |######################################################################| Time: 0:00:17
Loaded 1327 entries from dependency cache.
Parsing recipes: 100% |####################################################################| Time: 0:00:00
Parsing of 856 .bb files complete (855 cached, 1 parsed). 1328 targets, 80 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION        = "1.34.0"
BUILD_SYS         = "x86_64-linux"
NATIVELSBSTRING   = "universal"
TARGET_SYS        = "arm-poky-linux-gnueabi"
MACHINE           = "zybo-zynq7"
DISTRO            = "poky"
DISTRO_VERSION    = "2.3.3"
TUNE_FEATURES     = "arm armv7a vfp thumb neon callconvention-hard cortexa9"
TARGET_FPU        = "hard"
meta
meta-poky
meta-yocto-bsp    = "pyro:f21b7f5ae911eb8a0195937a20b92ebea442ab48"
meta-xilinx       = "pyro:b6462e55e65b44afed4b7a4e8b2af3381c961110"

Initialising tasks: 100% |#################################################################| Time: 0:00:00
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
NOTE: Tasks Summary: Attempted 2429 tasks of which 2429 didn't need to be rerun and all succeeded.
```

If the build is successful, the following files will be created under $TOPDIR/tmp/deploy/images/$MACHINE
```
root@b76ae5a3ca72:/home/build/poky/build/tmp/deploy/images/zybo-zynq7# ls
boot.bin
boot.bin-zybo-zynq7
boot.bin-zybo-zynq7-2017.01-r0
core-image-minimal-zybo-zynq7-20180119014655.rootfs.cpio
core-image-minimal-zybo-zynq7-20180119014655.rootfs.cpio.gz.u-boot
core-image-minimal-zybo-zynq7-20180119014655.rootfs.manifest
core-image-minimal-zybo-zynq7-20180119014655.rootfs.tar.gz
core-image-minimal-zybo-zynq7-20180119014655.testdata.json
core-image-minimal-zybo-zynq7.cpio
core-image-minimal-zybo-zynq7.cpio.gz.u-boot
core-image-minimal-zybo-zynq7.manifest
core-image-minimal-zybo-zynq7.tar.gz
core-image-minimal-zybo-zynq7.testdata.json
modules--4.9-xilinx-v2017.1+git0+68e6869cfb-r0-zybo-zynq7-20180119014655.tgz
modules-zybo-zynq7.tgz
u-boot.elf
u-boot.img
u-boot-zybo-zynq7-2017.01-r0.elf
u-boot-zybo-zynq7-2017.01-r0.img
u-boot-zybo-zynq7.elf
u-boot-zybo-zynq7.img
uEnv.txt
uImage
uImage--4.9-xilinx-v2017.1+git0+68e6869cfb-r0-zybo-zynq7-20180119014655.bin
uImage--4.9-xilinx-v2017.1+git0+68e6869cfb-r0-zynq-zybo-20180119014655.dtb
uImage-zybo-zynq7.bin
uImage-zynq-zybo.dtb
```

