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
Parsing recipes: 100% |####################################################################| Time: 0:00:33Parsing of 856 .bb files complete (0 cached, 856 parsed). 1328 targets, 80 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION        = "1.34.0"
BUILD_SYS         = "x86_64-linux"
NATIVELSBSTRING   = "ubuntu-16.04"
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

NOTE: Fetching uninative binary shim from http://downloads.yoctoproject.org/releases/uninative/1.7/x86_64-nativesdk-libc.tar.bz2;sha256sum=ed033c868b87852b07957a4400f3b744c00aef5d6470346ea1a59b6d3e03075e
--2018-01-18 08:32:48--  http://downloads.yoctoproject.org/releases/uninative/1.7/x86_64-nativesdk-libc.tar.bz2
Resolving downloads.yoctoproject.org (downloads.yoctoproject.org)... 198.145.29.63
Connecting to downloads.yoctoproject.org (downloads.yoctoproject.org)|198.145.29.63|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2286285 (2.2M) [application/octet-stream]
Saving to: ‘ /home/build/poky/build/downloads/uninative/ed033c868b87852b07957a4400f3b744c00aef5d6470346ea1a59b6d3e03075e/x86_64-nativesdk-libc.tar.bz2’


2018-01-18 08:32:49 (2.79 MB/s) - ‘ /home/build/poky/build/downloads/uninative/ed033c868b87852b07957a4400f3b744c00aef5d6470346ea1a59b6d3e03075e/x86_64-nativesdk-libc.tar.bz2’  saved [2286285/2286285]

Initialising tasks: 100% |#################################################################| Time: 0:00:03
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
...
...
...
Currently  4 running tasks (118 of 2429)   4% |##
```



