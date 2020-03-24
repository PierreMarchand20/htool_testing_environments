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
        gcc g++\
        clang\
        libblas-dev \
        liblapack-dev \
        libsuitesparse-dev \
        python3-pip python3-dev \
    && rm -rf /var/lib/apt/lists/* \
    && cd ~ \
    && wget https://cmake.org/files/v3.16/cmake-3.16.5.tar.gz \
    && tar -xzf cmake-3.16.5.tar.gz && cd cmake-3.16.5 \
    && ./bootstrap && make -j2 && make install \
    && cd .. && rm -r cmake-3.16.5.tar.gz cmake-3.16.5 \
    && pip3 --no-cache-dir install pytest wheel setuptools


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
