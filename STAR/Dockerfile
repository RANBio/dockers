FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
ENV WORK /work


RUN cd /work && \
  git clone https://github.com/alexdobin/STAR.git && \
  cd /work/STAR/source && \
  make STAR && \
  cp STAR /usr/local/bin

ENV RUN_CMD STAR
