# ===========================================================================================
# Dockerfile for building a Yocto-based distro for Altera
#-
# References:
#- https://rocketboards.org/foswiki/Documentation/GSRDCompilingLinux
# ===========================================================================================

FROM ubuntu:14.04

USER root

# Install the following utilities (required later)
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install phablet-tools sed wget cvs subversion git-core coreutils unzip texi2html  texinfo libsdl1.2-dev docbook-utils gawk python-pysqlite2 diffstat help2man  make gcc build-essential g++ desktop-file-utils chrpath libgl1-mesa-dev  libglu1-mesa-dev mercurial autoconf automake groff libtool xterm lib32z1 nano vim
RUN apt-get -y install lib32z1 lib32ncurses5 lib32bz2-1.0

# Fix error "Please use a locale setting which supports utf-8."
# See https://wiki.yoctoproject.org/wiki/TipsAndTricks/ResolvingLocaleIssues
RUN apt-get install -y locales
RUN locale-gen en_US.UTF-8
RUN \
        echo 'LANG="en_US.UTF-8"'>/etc/default/locale && \
        dpkg-reconfigure --frontend=noninteractive locales && \
        update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Get Yocto project for altera
RUN echo "wget http://releases.rocketboards.org/release/2019.04/src/altera.xml"                            >> bbsetup.sh \
 && echo "wget http://commondatastorage.googleapis.com/git-repo-downloads/repo"                            >> bbsetup.sh \
 && echo "chmod 777 repo"                                                                                  >> bbsetup.sh \
 && echo "git config --global user.name example                               "                            >> bbsetup.sh \
 && echo "git config --global user.email example@example.com                  "                            >> bbsetup.sh \
 && echo "repo init -u git://github.com/Angstrom-distribution/angstrom-manifest -b angstrom-v2018.12-thud" >> bbsetup.sh \
 && echo "mkdir -p .repo/local_manifests"                                                                  >> bbsetup.sh \
 && echo "mv altera.xml .repo/local_manifests/"                                                            >> bbsetup.sh \
 && echo "repo sync"                                                                                       >> bbsetup.sh

RUN echo "MACHINE=arria10 . ./setup-environment"                                                           >> env.sh \
 && echo "sed -i '/meta-altera/a \ \ \${TOPDIR}\/layers\/meta-altera-refdes \\' conf/bblayers.conf"         >> env.sh \
 && echo "sed -i '/meta-atmel/d' conf/bblayers.conf"                                                       >> env.sh \
 && echo "sed -i '/meta-freescale/d' conf/bblayers.conf"                                                   >> env.sh \
 && echo "echo \"DISTRO_FEATURES_remove = \" wayland \"\" >> conf/local.conf"                              >> env.sh \
 && echo "echo \"DISTRO_FEATURES_remove = \" alsa \"\" >> conf/local.conf"                                 >> env.sh \
 && echo "export KERNEL_PROVIDER=linux-altera-ltsi"                                                        >> env.sh \
 && echo "export KERNEL_TAG=refs/tags/ACDS19.1_REL_GSRD_PR"                                                >> env.sh \
 && echo "export KBRANCH=socfpga-4.14.130-ltsi"                                                            >> env.sh \
 && echo "export BB_ENV_EXTRAWHITE="$BB_ENV_EXTRAWHITE KBRANCH KERNEL_TAG UBOOT_TAG KERNEL_PROVIDER""      >> env.sh

# Define container entry point
ENTRYPOINT ["/bin/bash"]

# Expose sshd port
EXPOSE 22

# EOF
