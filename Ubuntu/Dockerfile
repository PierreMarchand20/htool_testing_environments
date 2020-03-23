FROM ubuntu:latest AS ubuntu_base

RUN apt-get update \
    && apt-get install -y  --no-install-recommends \
        ca-certificates \
        wget \
        libssl-dev \
        git \
        make \
        gcc \
        clang \
        libblas-dev \
        liblapack-dev \
        libsuitesparse-dev \
        python3-pip \
    && cd ~ \
    && wget https://cmake.org/files/v3.16/cmake-3.16.5.tar.gz \
    && tar -xzvf cmake-3.16.5.tar.gz && cd cmake-3.16.5 \
    && ./bootstrap && make -j2 && make install \
    && pip3 install pytest


FROM ubuntu_base AS ubuntu_openmpi

RUN apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev

FROM ubuntu_base AS ubuntu_mpich

RUN apt-get install -y  --no-install-recommends mpich libmpich-dev
