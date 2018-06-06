FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

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

RUN apt-get update && apt-get install -y libboost-all-dev

RUN cd /work && wget https://github.com/sparsehash/sparsehash/archive/sparsehash-2.0.3.tar.gz && \
    tar -xvzf sparsehash-2.0.3.tar.gz && \
    cd sparsehash-sparsehash-2.0.3/  && \
    ./configure --prefix=/usr/local/ && \
    make && \
    make install

RUN cd /work/ && wget https://sourceforge.net/projects/trowel-ec/files/src/trowel.0.1.4.3.src.tar.gz && \
    tar -xvzf trowel.0.1.4.3.src.tar.gz && \
    cd trowel.0.1.4.3.src && \
    ./autogen.sh && \
    cp trowel /usr/bin/


ENV RUN_CMD trowel

