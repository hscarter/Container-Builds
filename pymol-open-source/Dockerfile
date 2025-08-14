FROM ubuntu:22.04

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends --yes \
        ncat \
        vim \
        nano \
        emacs \
        xauth \
        tcl \
        lua5.3 \
        wget \
        ca-certificates \
        curl \
        pkg-config \
        make \
        autoconf \
        automake \
        cmake \
        binutils \
        websockify \
        xfce4 \
        at-spi2-core \
        xfce4-goodies \
        locales \
        dbus-x11

RUN locale-gen en_US.UTF-8
ENV LC_ALL="en_US.UTF-8"
ENV LANG="en_US.UTF-8"

# munge and slurm stuff
ARG MUNGEUSER=493
ARG MUNGEGROUP=493
ARG SLURMUSER=496
ARG SLURMGROUP=494
RUN groupadd -f -g $SLURMGROUP slurm \
    && useradd --no-create-home -u $SLURMUSER -g slurm  -s /bin/bash slurm
RUN groupadd -f -g $MUNGEGROUP munge \
    && useradd --no-create-home -u $MUNGEUSER -g munge -s /sbin/nologin munge

COPY ./turbovnc_2.2.5_amd64.deb /turbovnc_2.2.5_amd64.deb
RUN dpkg -i turbovnc_2.2.5_amd64.deb

#### end base image, start pymol ####

RUN apt-get install -y git build-essential python3-dev libglew-dev \
  libpng-dev libfreetype6-dev libxml2-dev \
  libmsgpack-dev python3-pyqt5.qtopengl \
  libglm-dev libnetcdf-dev

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN chmod +x /get-pip.py
RUN python3 -m get-pip


RUN git clone https://github.com/schrodinger/pymol-open-source.git
RUN git clone https://github.com/rcsb/mmtf-cpp.git
RUN mv mmtf-cpp/include/mmtf* pymol-open-source/include/
WORKDIR /pymol-open-source
RUN pip install .
WORKDIR /

