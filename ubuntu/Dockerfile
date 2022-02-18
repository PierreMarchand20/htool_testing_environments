FROM ubuntu:focal-20210119 AS ubuntu_base

WORKDIR /root

RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends \
    ca-certificates \
    wget \
    ssh \
    libssl-dev \
    git \
    make \
    cmake \
    gcc g++ gfortran lcov\
    clang \
    clang-format\
    libblas-dev \
    liblapack-dev \
    libsuitesparse-dev \
    libomp-dev \
    doxygen \
    python3-pip python3-dev\
    && pip3 --no-cache-dir install --upgrade pip \
    && pip3 --no-cache-dir install pytest wheel setuptools cmakelang scipy numpy \
    && rm -rf /var/lib/apt/lists/*


FROM ubuntu_base AS ubuntu_openmpi

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev \
    && pip3 --no-cache-dir install mpi4py \
    && rm -rf /var/lib/apt/lists/*

FROM ubuntu_base AS ubuntu_mpich

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends mpich libmpich-dev \
    && pip3 --no-cache-dir install mpi4py \
    && rm -rf /var/lib/apt/lists/*
