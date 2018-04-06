FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
ENV WORK /work

RUN cd /work && \
  wget http://research-pub.gene.com/gmap/src/gmap-gsnap-2018-03-25.tar.gz && \
  tar xvzf gmap-gsnap-2018-03-25.tar.gz &&\ 
  cd gmap-2018-03-25 && \
  ./configure --prefix=/usr/local/ && \
  make && \
  make install

ENV RUN_CMD gmap
