FROM ubuntu:focal-20210119 AS ubuntu_base

WORKDIR /root

RUN DEBIAN_FRONTEND="noninteractive" \
    TZ=Europe/Paris \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        wget \
        ssh \
        libssl-dev \
        git \
        make \
        cmake \
        gcc g++\
        clang\
        clang-format\
        libblas-dev \
        liblapack-dev \
        libsuitesparse-dev \
        python3-pip python3-dev\
        locales\
    && rm -rf /var/lib/apt/lists/* \
    && pip3 --no-cache-dir install pytest wheel setuptools cmakelang \
    # Set the locale
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.utf8

FROM ubuntu_base AS ubuntu_openmpi

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev \
    && rm -rf /var/lib/apt/lists/*

FROM ubuntu_base AS ubuntu_mpich

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends mpich libmpich-dev \
    && rm -rf /var/lib/apt/lists/*
