build-yocto-petalinux
===================

This subproject of easy-build provides a quick and easy way
for creating [Xilinx's PetaLinux](https://www.xilinx.com/products/design-tools/embedded-software/petalinux-sdk.html)
using the [Yocto project](http://www.yoctoproject.org) tools.

## Building container

    ./build.sh

## Running container

    ./run.sh

Create the build environment

    source setupsdk

Workaround: allow bitbake to run as root

    touch conf/sanity.conf

### Start the build
    MACHINE=zynqmp-generic bitbake petalinux-image-minimal

Sample output:
```
Parsing recipes: 100% |###################################################################################################################################| Time: 0:01:20
Parsing of 2463 .bb files complete (0 cached, 2463 parsed). 3256 targets, 228 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

Build Configuration:
BB_VERSION        = "1.32.0"
BUILD_SYS         = "x86_64-linux"
NATIVELSBSTRING   = "Ubuntu-16.04"
TARGET_SYS        = "aarch64-xilinx-linux"
MACHINE           = "zynqmp-generic"
DISTRO            = "petalinux"
DISTRO_VERSION    = "2017.4"
TUNE_FEATURES     = "aarch64"
TARGET_FPU        = ""
meta              
meta-poky         = "rel-v2017.4:8f6dfda5c3fe488e114033ba79230d944f3c2b90"
meta-perl         
meta-systemd      
meta-gpe          
meta-python       
meta-efl          
meta-ruby         
meta-filesystems  
meta-gnome        
meta-multimedia   
meta-networking   
meta-webserver    
meta-xfce         
meta-initramfs    
meta-oe           = "rel-v2017.4:53a3886699326c2e17b4a8072e63deb4ed6e662d"
meta-linaro-toolchain = "rel-v2017.4:39860f6c7af0858981cc004bbe4f4c421f6be607"
meta-qt5          = "rel-v2017.4:d67de10e2c589cb648095cbb59e946cf64979f0d"
meta-xilinx       = "rel-v2017.4:cdd0bf1e206922fad1826d818c463e6eae4f8388"
meta-xilinx-tools = "rel-v2017.4:460156a7bb428860418cd5ead2e5e27df4da9936"
meta-petalinux    = "rel-v2017.4:3f597b7a73437b6ed68422ba15b7f841662c3fa8"
meta-virtualization = "rel-v2017.4:af53de11b2d75e68b598c94cebe1a54f37450857"
meta-openamp      = "rel-v2017.4:20e02ea4c43c15dc3212519303ccaba3326db197"

NOTE: Fetching uninative binary shim from http://downloads.yoctoproject.org/releases/uninative/1.4/x86_64-nativesdk-libc.tar.bz2;sha256sum=101ff8f2580c193488db9e76f9646fb6ed38b65fb76f403acb0e2178ce7127ca
--2018-01-21 11:07:35--  http://downloads.yoctoproject.org/releases/uninative/1.4/x86_64-nativesdk-libc.tar.bz2
Resolving downloads.yoctoproject.org (downloads.yoctoproject.org)... 198.145.29.63
Connecting to downloads.yoctoproject.org (downloads.yoctoproject.org)|198.145.29.63|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2473216 (2.4M) [application/octet-stream]
Saving to: ‘/home/build/build/downloads/uninative/101ff8f2580c193488db9e76f9646fb6ed38b65fb76f403acb0e2178ce7127ca/x86_64-nativesdk-libc.tar.bz2’


2018-01-21 11:07:36 (3.01 MB/s) - ‘/home/build/build/downloads/uninative/101ff8f2580c193488db9e76f9646fb6ed38b65fb76f403acb0e2178ce7127ca/x86_64-nativesdk-libc.tar.bz2’ saved [2473216/2473216]

Initialising tasks: 100% |################################################################################################################################| Time: 0:00:03
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks

NOTE: Tasks Summary: Attempted 2190 tasks of which 10 didn't need to be rerun and all succeeded.

Summary: There were 2551 WARNING messages shown.
```
If the build is successful, the following files will be created under $TOPDIR/tmp/deploy/images/$MACHINE
```
root@9be0ed48fe4f:/home/build/build/tmp/deploy/images/zynqmp-generic# ls -al
total 151364
drwxr-xr-x 2 root root     4096 Jan 21 12:50 .
drwxr-xr-x 3 root root     4096 Jan 21 12:48 ..
-rw-r--r-- 2 root root    24608 Jan 21 12:50 arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.bin
-rw-r--r-- 2 root root    95152 Jan 21 12:50 arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.elf
-rw-r--r-- 2 root root    24672 Jan 21 12:50 arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.ub
lrwxrwxrwx 2 root root       84 Jan 21 12:50 arm-trusted-firmware.bin -> arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.bin
lrwxrwxrwx 2 root root       84 Jan 21 12:50 arm-trusted-firmware.elf -> arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.elf
lrwxrwxrwx 2 root root       83 Jan 21 12:50 arm-trusted-firmware.ub -> arm-trusted-firmware--1.3-xilinx-v2017.4+gitAUTOINC+47af34b94a-r0-20180121110734.ub
lrwxrwxrwx 2 root root       78 Jan 21 12:48 Image -> Image--4.9-xilinx-v2017.4+git0+b450e900fd-r0-zynqmp-generic-20180121110734.bin
-rw-r--r-- 2 root root 13310464 Jan 21 12:48 Image--4.9-xilinx-v2017.4+git0+b450e900fd-r0-zynqmp-generic-20180121110734.bin
lrwxrwxrwx 2 root root       78 Jan 21 12:48 Image-zynqmp-generic.bin -> Image--4.9-xilinx-v2017.4+git0+b450e900fd-r0-zynqmp-generic-20180121110734.bin
-rw-r--r-- 2 root root  9494224 Jan 21 12:48 modules--4.9-xilinx-v2017.4+git0+b450e900fd-r0-zynqmp-generic-20180121110734.tgz
lrwxrwxrwx 2 root root       80 Jan 21 12:48 modules-zynqmp-generic.tgz -> modules--4.9-xilinx-v2017.4+git0+b450e900fd-r0-zynqmp-generic-20180121110734.tgz
-rw-r--r-- 2 root root 23310336 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio
-rw-r--r-- 2 root root 10914910 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio.gz
-rw-r--r-- 2 root root 10914974 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio.gz.u-boot
-rw-r--r-- 2 root root 67108864 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext3
-rw-r--r-- 2 root root 67108864 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext4
-rw-r--r-- 2 root root 10968802 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext4.gz
-rw-r--r-- 2 root root 13107200 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.jffs2
-rw-r--r-- 2 root root     5187 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.manifest
-rw-r--r-- 2 root root 10924501 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.tar.gz
lrwxrwxrwx 2 root root       65 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic.cpio -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio
lrwxrwxrwx 2 root root       68 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic.cpio.gz -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio.gz
lrwxrwxrwx 2 root root       75 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic.cpio.gz.u-boot -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.cpio.gz.u-boot
lrwxrwxrwx 2 root root       65 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic.ext3 -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext3
lrwxrwxrwx 2 root root       65 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic.ext4 -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext4
lrwxrwxrwx 2 root root       68 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic.ext4.gz -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.ext4.gz
lrwxrwxrwx 2 root root       66 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic.jffs2 -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.jffs2
lrwxrwxrwx 2 root root       69 Jan 21 12:49 petalinux-image-minimal-zynqmp-generic.manifest -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.manifest
lrwxrwxrwx 2 root root       67 Jan 21 12:50 petalinux-image-minimal-zynqmp-generic.tar.gz -> petalinux-image-minimal-zynqmp-generic-20180121110734.rootfs.tar.gz
-rw-r--r-- 2 root root      294 Jan 21 12:48 README_-_DO_NOT_DELETE_FILES_IN_THIS_DIRECTORY.txt
```

