# ===========================================================================================
# Dockerfile for building a Yocto-based distro for Xilinx
#-
# References:
#   https://github.com/gmacario/easy-build/tree/master/build-yocto-fsl-arm
# ===========================================================================================

FROM tethys/build-yocto

USER root

# Install the following utilities (required later)
RUN apt-get -y install nano vim libsdl1.2-dev xterm \
             crossbuild-essential-armhf device-tree-compiler libssl-dev

# Get Yocto project for xilinx
RUN git clone -b pyro git://git.yoctoproject.org/poky.git
RUN git clone -b pyro git://git.yoctoproject.org/meta-xilinx.git

# Define container entry point
ENTRYPOINT ["/bin/bash"]

# Expose sshd port
EXPOSE 22

# EOF
