# ===========================================================================================
# Dockerfile for building PetaLinux 
# References:
#   http://www.wiki.xilinx.com/Getting+started+with+Yocto+Xilinx+layer
# ===========================================================================================

FROM tethys/build-yocto

USER root

# Xilinx Version
ARG XILINX_VER="rel-v2017.4"

# Install the following utilities (required later)
RUN apt-get -y install curl nano vim

# Install "repo" tool
RUN curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo
RUN chmod a+x /usr/local/bin/repo

# Fetch PetaLinux sources
RUN repo init -u git://github.com/Xilinx/yocto-manifests.git -b ${XILINX_VER} \
    && repo sync \
    && repo start ${XILINX_VER} --all

# Define container entry point
ENTRYPOINT ["/bin/bash"]

# Expose sshd port
EXPOSE 22

# EOF
