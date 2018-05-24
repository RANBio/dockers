FROM rcents/im:base

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

# get ubuntu packages
# incl python matplotlib for preqc
RUN apt-get update && \
     apt-get install -y \
         autotools-dev \
         libjemalloc-dev \
         libsparsehash-dev \
         libjsoncpp-dev \
         libz-dev \
         python-matplotlib

# build remaining dependencies:
# bamtools
RUN mkdir -p /work/ && \
     cd /work/ && \
     wget https://github.com/pezmaster31/bamtools/archive/v2.5.1.tar.gz && \
     tar -xzvf v2.5.1.tar.gz && \
     rm v2.5.1.tar.gz && \
     cd bamtools-2.5.1 && \
     mkdir build && \
     cd build && \
     cmake .. && \
     make && \
     make install
# RUN git clone git://github.com/pezmaster31/bamtools.git && \
# apt -y install bamtools

# build SGA
RUN mkdir -p /src && \
     cd /src && \
     wget https://github.com/jts/sga/archive/v0.10.15.tar.gz && \
     tar -xzvf v0.10.15.tar.gz && \
     rm v0.10.15.tar.gz && \
     cd sga-0.10.15/src && \
     ./autogen.sh && \
     #./configure --with-jemalloc=/usr --prefix=/usr/local && \
     ./configure --with-bamtools=/usr/local/ --with-jemalloc=/usr --prefix=/usr/local && \
     make && \
     make install

RUN cd /work/ && \
    git clone https://github.com/hillerlab/IterativeErrorCorrection.git && \
    cp IterativeErrorCorrection/SGA-ICE.py /usr/local/bin/

