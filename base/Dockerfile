FROM debian:stable

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# update 
RUN apt-get update && apt-get dist-upgrade -y

# Basic dependencies
RUN apt-get update -y && \
  apt-get install -y --no-install-recommends \
  apt-utils \
  automake \
  ant \
  bash \
  binutils \
  perl \
  build-essential \
  bzip2 \
  c++11 \
  cdbs \
  cmake \
  cron \
  curl \
  dkms \
  dpkg-dev \
  g++ \
  gpp \
  gcc \
  gfortran \
  git \
  git-core \
  libblas-dev \
  libatlas-dev \
  libbz2-dev \
  liblzma-dev \
  libpcre3-dev \
  libreadline-dev \
  make \
  mercurial \
  python python-dev python-yaml ncurses-dev zlib1g-dev python-numpy python-pip \
  sudo \
  tree \
  unzip \
  vim \
  wget \
  libc-bin \
  llvm \
  libconfig-dev \
  ncurses-dev \
  zlib1g-dev 


EXPOSE 8080

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/


