FROM debian:latest AS debian_base

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends \
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
        python3-pip python3-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 --no-cache-dir install pytest wheel setuptools cmakelang


FROM debian_base AS debian_openmpi

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev \
    && rm -rf /var/lib/apt/lists/*

FROM debian_base AS debian_mpich

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends mpich libmpich-dev \
    && rm -rf /var/lib/apt/lists/*
