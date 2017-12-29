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


ENV RUN_CMD bfc
