FROM debian:buster-20200908-slim AS debian_base

WORKDIR /root

RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y  --no-install-recommends \
        ca-certificates \
        wget \
        ssh \
        libssl-dev \
        git \
        make \
        cmake \
        gcc g++ lcov\
        clang\
        clang-format\
        libblas-dev \
        liblapack-dev \
        libsuitesparse-dev \
        python3-pip python3-dev \
        # needed for openmp with clang
        libomp-dev \
    && pip3 --no-cache-dir install pytest wheel setuptools cmakelang

FROM debian_base AS debian_openmpi

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends openmpi-bin libopenmpi-dev \
    && pip3 --no-cache-dir install mpi4py \
    && rm -rf /var/lib/apt/lists/*

FROM debian_base AS debian_mpich

WORKDIR /root

RUN apt-get update \
    && apt-get install -y  --no-install-recommends mpich libmpich-dev \
    && pip3 --no-cache-dir install mpi4py \
    && rm -rf /var/lib/apt/lists/*
