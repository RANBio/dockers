FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
ENV WORK /work


RUN cd /work && \
  git clone https://github.com/infphilo/hisat2.git && \
  cd /work/hisat2 && \
  make && \
  cp hisat2 hisat2-align-s hisat2-align-l \
     hisat2-build hisat2-build-s hisat2-build-l \
     hisat2-inspect hisat2-inspect-s hisat2-inspect-l \
     /usr/local/bin/

ENV RUN_CMD hisat2
