FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
ENV WORK /work

RUN cd /work && \
   wget http://www.csd.uwo.ca/~ilie/RACER/racer.zip && \
   unzip racer.zip && \
   make -f Makefile_parallel && \
   cp RACER /usr/local/bin/

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

RUN cd /work && \
   git clone https://github.com/lucian-ilie/Correcting-Illumina-data.git && \
   cd /work/Correcting-Illumina-data/readSearch && \
   make && \
   cp readSearch /usr/local/bin && \
   cd /work/Correcting-Illumina-data/kmerSearch && \
   make && \
   cp kmerSearch /usr/local/bin

ENV RUN_CMD RACER
