FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

ENV WORK /work

RUN cd /work && \
  wget https://github.com/01org/tbb/archive/2018_U2.tar.gz && \
  tar xzf 2018_U2.tar.gz && \
  cd tbb-2018_U2 && \
  make && \
  cp -r include/tbb /usr/include/ && \
  cp build/*_release/*.so /usr/lib/ && \
  cp build/*_release/*.so.* /usr/lib/ 

RUN cd /work && \
    wget https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.gz && \
    tar xvzf boost_1_66_0.tar.gz && \
    cd /work//boost_1_66_0/ && \
    ./bootstrap.sh && \
    ./b2 install


RUN cd /work && \
  git clone https://github.com/kingsfordgroup/sailfish.git && \
  cd /work/sailfish && \
  mkdir build && \
  cd build && \
  cmake .. -DBOOST_ROOT=/usr/local/ -DTBB_INSTALL_DIR=/usr/ -DCMAKE_INSTALL_PREFIX=/usr/local && \
  make && \
  make install

ENV RUN_CMD sailfish
