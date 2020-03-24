FROM debian:latest AS debian_base

RUN apt-get update \
    && apt-get install -y  --no-install-recommends \
        ca-certificates \
        wget \
        libssl-dev \
        git \
        make \
        gcc g++\
        clang \
        libblas-dev \
        liblapack-dev \
        libsuitesparse-dev \
        python3-pip python3-dev \
    && cd ~ \
    && wget https://cmake.org/files/v3.16/cmake-3.16.5.tar.gz \
    && tar -xzf cmake-3.16.5.tar.gz && cd cmake-3.16.5 \
    && ./bootstrap && make -j2 && make install \
    && pip3 install pytest wheel setuptools


FROM debian_base AS debian_openmpi

RUN apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev

FROM debian_base AS debian_mpich

RUN apt-get install -y  --no-install-recommends mpich libmpich-dev
