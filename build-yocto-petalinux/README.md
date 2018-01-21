build-yocto-petalinux
===================

This subproject of easy-build provides a quick and easy way
for creating Xilinx's PetaLinux
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

```

