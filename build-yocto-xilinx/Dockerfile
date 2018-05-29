# ===========================================================================================
# Dockerfile for building a Yocto-based distro for Xilinx
#-
# References:
#   https://github.com/gmacario/easy-build/tree/master/build-yocto-fsl-arm
# ===========================================================================================

FROM tethys/build-yocto

USER root

# Install the following utilities (required later)
RUN apt-get -y install nano vim

# Get Yocto project for xilinx
RUN git clone -b sumo git://git.yoctoproject.org/poky.git \
&&  cd poky \
&&  git clone git://github.com/hiiaka/meta-xilinx.git

# Define container entry point
ENTRYPOINT ["/bin/bash"]

# Expose sshd port
EXPOSE 22

# EOF
