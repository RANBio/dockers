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

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

# runtime dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    tcl \
    tk \
  && rm -rf /var/lib/apt/lists/*

ENV GPG_KEY C01E1CAD5EA2C4F0B8E3571504C367C218ADD4FF
ENV PYTHON_VERSION 2.7.14

RUN set -ex \
  && buildDeps=' \
    dpkg-dev \
    tcl-dev \
    tk-dev \
  ' \
  && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
  \
  && wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
  && wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
  && export GNUPGHOME="$(mktemp -d)" \
  && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
  && gpg --batch --verify python.tar.xz.asc python.tar.xz \
  && rm -rf "$GNUPGHOME" python.tar.xz.asc \
  && mkdir -p /usr/src/python \
  && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
  && rm python.tar.xz \
  \
  && cd /usr/src/python \
  && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
  && ./configure \
    --build="$gnuArch" \
    --enable-shared \
    --enable-unicode=ucs4 \
  && make -j "$(nproc)" \
  && make install \
  && ldconfig \
  \
  && apt-get purge -y $buildDeps \
  \
  && find /usr/local -depth \
    \( \
      \( -type d -a \( -name test -o -name tests \) \) \
      -o \
      \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
    \) -exec rm -rf '{}' + \
  && rm -rf /usr/src/python

# if this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ENV PYTHON_PIP_VERSION 9.0.1

RUN set -ex; \
  \
  wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
  \
  python get-pip.py \
    --disable-pip-version-check \
    --no-cache-dir \
    "pip==$PYTHON_PIP_VERSION" \
  ; \
  pip --version; \
  \
  find /usr/local -depth \
    \( \
      \( -type d -a \( -name test -o -name tests \) \) \
      -o \
      \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
    \) -exec rm -rf '{}' +; \
  rm -f get-pip.py

# install "virtualenv", since the vast majority of users of this image will want it
RUN pip install --no-cache-dir virtualenv

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


RUN cd /work/ && \
  git clone https://github.com/RCENTS/samutils.git && \
  cd samutils && \
  python setup.py install

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
