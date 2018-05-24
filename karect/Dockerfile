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
RUN wget https://github.com/aminallam/karect/tarball/master && \
    tar -xzvf master && \
    cd aminallam-karect-ba3ad54 && \
    make && \
    cp karect /usr/local/bin;

