FROM debian:stretch

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
RUN mkdir /work
ENV WORK /work

# wget and curl etc .
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    wget \
  && rm -rf /var/lib/apt/lists/*

RUN set -ex; \
  if ! command -v gpg > /dev/null; then \
    apt-get update; \
    apt-get install -y --no-install-recommends \
      gnupg \
      dirmngr \
    ; \
    rm -rf /var/lib/apt/lists/*; \
fi

# scm etc.
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    git-core \
    mercurial \
    openssh-client \
  && rm -rf /var/lib/apt/lists/*

# build dependencies
RUN set ex; \
  apt-get update -y; \
  apt-get install -y --no-install-recommends \
  apt-utils \
  autoconf \
  automake \
  bash \
  binutils \
  build-essential \
  bzip2 \
  cmake \
  dpkg-dev \
  g++-6 \
  gcc-6 \
  gfortran-6 \
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
  libxml2-dev \
  make \
  mercurial \
  ncurses-dev \
  patch \
  perl \
  sudo \
  tree \
  unzip \
  wget \
  zlib1g-dev

RUN which g++
#  python python-dev zlib1g-dev python-numpy python-pip \
# install python from the source : taken from  https://github.com/docker-library/python
# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

#install python pip
RUN apt-get update -y && apt-get install -y python-pip

# upgrade java and set java home
RUN apt-get update -y && apt-get install -y openjdk-8-jdk openjdk-8-doc openjdk-8-jre

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
ENV PATH $PATH:/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
RUN sed -i 'aPATH=$PATH:/usr/lib/jvm/java-8-openjdk-amd64/jre/bin' /root/.bashrc

# install samtools
ENV PERL5LIB "."
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

RUN mkdir -p /root/.ncbi && \
  echo '/repository/user/main/public/root = "/data/"' > /root/.ncbi/user-settings.mkfg

RUN cd /work/ngs/ngs-python && \
  python setup.py install && \
  cp /usr/local/ncbi/sra-tools/bin/* /usr/local/bin

# python libraries
RUN pip install Scons && \
  pip install pysam


#
# install nextflow
RUN cd /usr/local/bin && curl -s https://get.nextflow.io | bash 

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ && \
    rm -rf /work/*

# RUN samtools --help
# RUN fastq-dump --help
# RUN ls /work     /
