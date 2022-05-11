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
    gcc g++ gfortran lcov\
    clang\
    clang-format\
    libblas-dev \
    liblapack-dev \
    libsuitesparse-dev \
    python3-pip python3-dev \
    # needed for openmp with clang
    libomp-dev \
    doxygen \
    && pip3 --no-cache-dir install --upgrade pip \
    && pip3 --no-cache-dir install pytest wheel setuptools cmakelang scipy numpy \
    && rm -rf /var/lib/apt/lists/*

FROM debian_base AS debian_gcc_openmpi

# Build Options:
# These options are passed to the steps below
ARG OPENMPI_VERSION="4.1.3"
ARG OPENMPI_MAJOR_VERSION="v4.1"
ARG OPENMPI_CONFIGURE_OPTIONS
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
    && cd && rm -rf /tmp/openmpi-src && ldconfig \
    && pip3 --no-cache-dir install mpi4py 

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}

FROM debian_base AS debian_clang_openmpi

# Build Options:
# These options are passed to the steps below
ARG OPENMPI_VERSION="4.1.3"
ARG OPENMPI_MAJOR_VERSION="v4.1"
ARG OPENMPI_CONFIGURE_OPTIONS
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
    && cd && rm -rf /tmp/openmpi-src && ldconfig \
    && pip3 --no-cache-dir install mpi4py 

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}

FROM debian_base AS debian_gcc_mpich

# Build Options:
# See installation guide of target MPICH version
# Ex: http://www.mpich.org/static/downloads/3.4/mpich-3.4-installguide.pdf
# These options are passed to the steps below
ARG MPICH_VERSION="4.0.2"
ARG MPICH_CONFIGURE_OPTIONS="--with-device=ch4:ofi --disable-f77"
ARG MPICH_MAKE_OPTIONS="-j4"

# Download, build, and install MPICH
RUN mkdir /tmp/mpich-src && cd /tmp/mpich-src \
    && wget http://www.mpich.org/static/downloads/${MPICH_VERSION}/mpich-${MPICH_VERSION}.tar.gz \
    && tar xfz mpich-${MPICH_VERSION}.tar.gz \
    && cd mpich-${MPICH_VERSION} \
    && CC=gcc CXX=g++ ./configure ${MPICH_CONFIGURE_OPTIONS} \
    && make ${MPICH_MAKE_OPTIONS} \
    && make install \
    && rm -rf /tmp/mpich-src && ldconfig \
    && pip3 --no-cache-dir install mpi4py 

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}

FROM debian_base AS debian_clang_mpich

# Build Options:
# See installation guide of target MPICH version
# Ex: http://www.mpich.org/static/downloads/3.4/mpich-3.4-installguide.pdf
# These options are passed to the steps below
ARG MPICH_VERSION="4.0.2"
ARG MPICH_CONFIGURE_OPTIONS="--with-device=ch4:ofi --disable-f77"
ARG MPICH_MAKE_OPTIONS="-j4"

# Download, build, and install MPICH
RUN mkdir /tmp/mpich-src && cd /tmp/mpich-src \
    &&  wget http://www.mpich.org/static/downloads/${MPICH_VERSION}/mpich-${MPICH_VERSION}.tar.gz \
    && tar xfz mpich-${MPICH_VERSION}.tar.gz \
    && cd mpich-${MPICH_VERSION}  \
    && CC=clang CXX=clang++ ./configure ${MPICH_CONFIGURE_OPTIONS} \
    && make ${MPICH_MAKE_OPTIONS} \
    && make install \
    && rm -rf /tmp/mpich-src && ldconfig \
    && pip3 --no-cache-dir install mpi4py 

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
ENV USER_HOME /home/${USER}
RUN useradd -s /bin/bash --user-group --system --create-home --no-log-init ${USER}

USER ${USER}
WORKDIR ${USER_HOME}
