FROM rcents/im:base

MAINTAINER Sriram P C sriram.pc@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# work dir
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
  git clone https://github.com/BenLangmead/bowtie2.git && \
  cd /work/bowtie2 && \
  make && \
  cp bowtie2* /usr/local/bin

RUN cd /work && \
    wget https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.gz && \
    tar xvzf boost_1_66_0.tar.gz && \
    cd /work//boost_1_66_0/ && \
    ./bootstrap.sh && \
    ./b2 install

RUN cd /work && \
  git clone https://github.com/infphilo/tophat.git && \
  cd /work/tophat && \
  ./autogen.sh && \
  ./configure && \
  sed -i '341s/<Junction, JunctionStats>//' src/juncs_db.cpp && \
  sed -i '2708s/<Junction, JunctionStats>//' src/tophat_reports.cpp && \
  make && \
  make install 

ENV RUN_CMD tophat
