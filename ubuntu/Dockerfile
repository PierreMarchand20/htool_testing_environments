FROM ubuntu:noble-20240605 AS ubuntu_base

WORKDIR /root

RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends \
    ca-certificates \
    locales \
    wget \
    ssh \
    libssl-dev \
    git \
    make \
    cmake \
    gcc g++ gfortran lcov\
    clang\
    libclang-rt-18-dev\
    # needed for sanitizers with clang
    clang-format\
    clang-tidy\
    libblas-dev \
    liblapack-dev \
    libsuitesparse-dev \
    libomp-dev \
    doxygen \
    python3-pip python3-dev python3-venv


FROM ubuntu_base AS ubuntu_gcc_openmpi

# Build Options:
# These options are passed to the steps below
ARG OPENMPI_VERSION="5.0.5"
ARG OPENMPI_MAJOR_VERSION="v5.0"
ARG OPENMPI_CONFIGURE_OPTIONS=""
ARG OPENMPI_MAKE_OPTIONS="-j4"

# Download, build, and install OPENMPI
RUN mkdir /tmp/openmpi-src \
    && cd /tmp/openmpi-src \
    && wget https://download.open-mpi.org/release/open-mpi/${OPENMPI_MAJOR_VERSION}/openmpi-${OPENMPI_VERSION}.tar.gz \
    && tar xfz openmpi-${OPENMPI_VERSION}.tar.gz \
    && cd openmpi-${OPENMPI_VERSION} \
    && CC=gcc CXX=g++ ./configure ${OPENMPI_CONFIGURE_OPTIONS} \
    && make all ${OPENMPI_MAKE_OPTIONS} \ 
    && make install \
    && cd && rm -rf /tmp/openmpi-src && ldconfig

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}

FROM ubuntu_base AS ubuntu_clang_openmpi

# Build Options:
# These options are passed to the steps below
ARG OPENMPI_VERSION="5.0.5"
ARG OPENMPI_MAJOR_VERSION="v5.0"
ARG OPENMPI_CONFIGURE_OPTIONS=""
ARG OPENMPI_MAKE_OPTIONS="-j4"

# Download, build, and install OPENMPI
RUN mkdir /tmp/openmpi-src \
    && cd /tmp/openmpi-src \
    && wget https://download.open-mpi.org/release/open-mpi/${OPENMPI_MAJOR_VERSION}/openmpi-${OPENMPI_VERSION}.tar.gz \
    && tar xfz openmpi-${OPENMPI_VERSION}.tar.gz \
    && cd openmpi-${OPENMPI_VERSION} \
    && CC=clang CXX=clang++ ./configure ${OPENMPI_CONFIGURE_OPTIONS} \
    && make all ${OPENMPI_MAKE_OPTIONS} \ 
    && make install \
    && cd && rm -rf /tmp/openmpi-src && ldconfig

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}


FROM ubuntu_base AS ubuntu_gcc_mpich

# Build Options:
# See installation guide of target MPICH version
# Ex: http://www.mpich.org/static/downloads/3.4/mpich-3.4-installguide.pdf
# These options are passed to the steps below
ARG MPICH_VERSION="4.2.2"
ARG MPICH_CONFIGURE_OPTIONS="FFLAGS=-fallow-argument-mismatch FCFLAGS=-fallow-argument-mismatch  --enable-shared"
ARG MPICH_MAKE_OPTIONS="-j4"

# Download, build, and install MPICH
RUN mkdir /tmp/mpich-src && cd /tmp/mpich-src \
    && wget http://www.mpich.org/static/downloads/${MPICH_VERSION}/mpich-${MPICH_VERSION}.tar.gz \
    && tar xfz mpich-${MPICH_VERSION}.tar.gz \
    && cd mpich-${MPICH_VERSION} \
    && CC=gcc CXX=g++ ./configure ${MPICH_CONFIGURE_OPTIONS} \
    && make ${MPICH_MAKE_OPTIONS} \
    && make install \
    && cd && rm -rf /tmp/mpich-src && ldconfig

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}

FROM ubuntu_base AS ubuntu_clang_mpich

# See installation guide of target MPICH version
# Ex: http://www.mpich.org/static/downloads/3.4/mpich-3.4-installguide.pdf
# These options are passed to the steps below
ARG MPICH_VERSION="4.2.2"
ARG MPICH_CONFIGURE_OPTIONS="FFLAGS=-fallow-argument-mismatch FCFLAGS=-fallow-argument-mismatch --enable-shared"
ARG MPICH_MAKE_OPTIONS="-j4"

# Download, build, and install MPICH
RUN mkdir /tmp/mpich-src && cd /tmp/mpich-src \
    &&  wget http://www.mpich.org/static/downloads/${MPICH_VERSION}/mpich-${MPICH_VERSION}.tar.gz \
    && tar xfz mpich-${MPICH_VERSION}.tar.gz \
    && cd mpich-${MPICH_VERSION}  \
    && CC=clang CXX=clang++ ./configure ${MPICH_CONFIGURE_OPTIONS} \
    && make ${MPICH_MAKE_OPTIONS} \
    && make install \
    && cd && rm -rf /tmp/mpich-src && ldconfig

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}
