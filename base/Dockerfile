FROM debian:jessie

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
RUN mkdir /work
ENV WORK /work

# update 
RUN apt-get update && apt-get dist-upgrade -y

# Basic dependencies
RUN apt-get update -y && \
  apt-get install -y --no-install-recommends \
  apt-utils \
  automake \
  bash \
  binutils \
  build-essential \
  bzip2 \
  c++11 \
  cmake \
  cron \
  curl \
  dpkg-dev \
  g++ \
  gcc \
  gfortran \
  git \
  git-core \
  openssl \
  libatlas-dev \
  libblas-dev \
  libbz2-dev \
  libc-bin \
  libconfig-dev \
  libcurl4-openssl-dev \
  liblzma-dev \
  libpcre3-dev \
  libreadline-dev \
  libssl-dev \
  make \
  mercurial \
  ncurses-dev \
  perl \
  python python-dev zlib1g-dev python-numpy python-pip \
  sudo \
  tree \
  unzip \
  wget \
  zlib1g-dev

# upgrade java
RUN apt-get install -y openjdk-7-jdk openjdk-7-doc openjdk-7-jre-lib

# set java home
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java
RUN sed -i 'aPATH=$PATH:/usr/lib/jvm/java-7-openjdk-amd64/jre/bin' /root/.bashrc

# install samtools
RUN cd /work && \
  git clone git://github.com/samtools/htslib.git && \
  git clone git://github.com/samtools/bcftools.git && \
  git clone git://github.com/samtools/samtools.git && \
  cd /work/htslib && \
  autoheader && \
  autoconf && \
  ./configure && \
  make && \
  make install && \
  cd /work/bcftools && \
  autoheader && \
  autoconf && \
  ./configure && \
  make && \
  make install && \
  cd /work/samtools && \
  autoheader && \
  autoconf && \
  ./configure && \
  make && \
  make install

# install sra tools
RUN cd /work && \
  git clone git://github.com/ncbi/ngs.git && \
  git clone git://github.com/ncbi/ncbi-vdb.git && \
  git clone git://github.com/ncbi/sra-tools.git && \
  cd /work/ncbi-vdb && \
  ./configure --build-prefix=/work/ncbi-outdir && \
  make && \
  make install && \
  cd /work/ngs && \
  ./configure --build-prefix=/work/ncbi-outdir && \
  make && \
  make install && \
  cd /work/sra-tools  && \
  ./configure --build-prefix=/work/ncbi-outdir && \
  make && \
  make install

RUN cd /work/ngs/ngs-python && \
  python setup.py install && \
  cp /usr/local/ncbi/sra-tools/bin/* /usr/local/bin

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ && \
    rm -rf /work/*

# RUN samtools --help
# RUN fastq-dump --help
# RUN ls /work     /
