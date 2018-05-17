# ===========================================================================================
# Dockerfile for building development for SoCFPGAs
#-
# ===========================================================================================

FROM tethys/build-yocto

USER root
# Set ARGs
ARG PRJROOT="FPGA-SoC"
ARG PRJLINX=${PRJROOT}"-Linux"

ARG ROOT_VER="v0.8.0"
# ARG ZYBO="ZYBO"
ARG ZYBO="ZYBO""-Z7"
ARG PYNQ="PYNQ-Z1"
ARG DE0="DE0-Nano-SoC"

RUN echo ${ZYBO}
# Install the following utilities (required later)
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash \
    && apt-get update && apt-get -y upgrade \
    && apt-get -y install \
        nano vim  \
        bc crossbuild-essential-armhf device-tree-compiler libssl-dev \
        git-lfs


# Get FPGA-SoC-Linux project
RUN git clone --depth=1 --branch ${ROOT_VER}  git://github.com/ikwzm/${PRJLINX} \
    && cd ${PRJLINX} \
    && git lfs pull \
    &&  echo ""

# Get FPGA-SoC-Linux U-boot build project
RUN for i in ${PYNQ} ${DE0} ${ZYBO};  do git clone --depth=1 https://github.com/ikwzm/${PRJROOT}-U-Boot-${i}.git ; done

# Define container entry point
ENTRYPOINT ["/bin/bash"]

# Expose sshd port
EXPOSE 22

# EOF
