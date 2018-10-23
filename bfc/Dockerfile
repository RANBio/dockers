FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
ENV WORK /work

RUN cd /work && \
  git clone git://github.com/lh3/bfc.git && \
  cd /work/bfc && \
  make && \
  cp bfc /usr/local/bin/

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

RUN cd /work && \
  git clone https://github.com/lh3/seqtk.git && \
  cd /work/seqtk && \
  make && \
  cp seqtk /usr/local/bin 

ENV RUN_CMD bfc
