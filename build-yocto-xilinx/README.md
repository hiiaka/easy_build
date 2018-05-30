build-yocto-xilinx
===================

This subproject of easy-build provides a quick and easy way
for creating embedded Linux distributions for Xilinx FPGA
using the [Yocto project](http://www.yoctoproject.org) tools.

## Building container

    ./build.sh

## Running container

    ./run.sh

Create the build environment-

    cd poky
    source oe-init-build-env

Workaround: allow bitbake to run as root

    touch conf/sanity.conf

Add Xilinx's bblayers

    bitbake-layers add-layer ../poky/meta-xilinx/meta-xilinx-bsp
    bitbake-layers add-layer ../poky/meta-xilinx/meta-xilinx-contrib

    cat conf/bblayer.conf

    # POKY_BBLAYERS_CONF_VERSION is increased each time build/conf/bblayers.conf
    # changes incompatibly
    POKY_BBLAYERS_CONF_VERSION = "2"

    BBPATH = "${TOPDIR}"
    BBFILES ?= ""

    BBLAYERS ?= " \
      /home/build/poky/meta \
      /home/build/poky/meta-poky \
      /home/build/poky/meta-yocto-bsp \
      /home/build/poky/meta-xilinx/meta-xilinx-bsp \
      /home/build/poky/meta-xilinx/meta-xilinx-contrib \
      "

### Start the build
    MACHINE=zybo-zynq7 bitbake core-image-minimal

Sample output:
```
Loaded 1308 entries from dependency cache.
Parsing recipes: 100% |###########################################################################################################| Time: 0:00:00
Parsing of 847 .bb files complete (846 cached, 1 parsed). 1309 targets, 81 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION           = "1.36.0"
BUILD_SYS            = "x86_64-linux"
NATIVELSBSTRING      = "universal"
TARGET_SYS           = "arm-poky-linux-gnueabi"
MACHINE              = "zybo-zynq7"
DISTRO               = "poky"
DISTRO_VERSION       = "2.4.3"
TUNE_FEATURES        = "arm armv7a vfp thumb neon callconvention-hard cortexa9"
TARGET_FPU           = "hard"
meta                 
meta-poky            
meta-yocto-bsp       = "rocko:7e7ee662f5dea4d090293045f7498093322802cc"
meta-xilinx-bsp      
meta-xilinx-contrib  = "master:1e5fda195b960687e9414ba125cf4f3499cd6052"

Initialising tasks: 100% |########################################################################################################| Time: 0:00:02
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
NOTE: Tasks Summary: Attempted 2475 tasks of which 2475 didn't need to be rerun and all succeeded.
```

If the build is successful, the following files will be created under $TOPDIR/tmp/deploy/images/$MACHINE
```
root@f35aa5e7827e:/home/build/build/tmp/deploy/images/zybo-zynq7# ls
boot.bin
boot.bin-zybo-zynq7
boot.bin-zybo-zynq7-2017.09-r0
core-image-minimal-zybo-zynq7-20180525231304.rootfs.cpio
core-image-minimal-zybo-zynq7-20180525231304.rootfs.cpio.gz.u-boot
core-image-minimal-zybo-zynq7-20180525231304.rootfs.manifest
core-image-minimal-zybo-zynq7-20180525231304.rootfs.tar.gz
core-image-minimal-zybo-zynq7-20180525231304.testdata.json
core-image-minimal-zybo-zynq7.cpio
core-image-minimal-zybo-zynq7.cpio.gz.u-boot
core-image-minimal-zybo-zynq7.manifest
core-image-minimal-zybo-zynq7.tar.gz
core-image-minimal-zybo-zynq7.testdata.json
modules--4.14-xilinx-v2018.1+git0+4ac76ffacb-r0-zybo-zynq7-20180525231304.tgz
modules-zybo-zynq7.tgz
u-boot.elf
u-boot.img
u-boot-zybo-zynq7-2017.09-r0.elf
u-boot-zybo-zynq7-2017.09-r0.img
u-boot-zybo-zynq7.elf
u-boot-zybo-zynq7.img
uEnv.txt
uImage
uImage--4.14-xilinx-v2018.1+git0+4ac76ffacb-r0-zybo-zynq7-20180525231304.bin
uImage--4.14-xilinx-v2018.1+git0+4ac76ffacb-r0-zynq-zybo-20180525231304.dtb
uImage-zybo-zynq7.bin
uImage-zynq-zybo.dtb
zynq-zybo.dtb
```

