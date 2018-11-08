FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

RUN apt-get -y update && apt-get -y install libboost-all-dev 

RUN cd /work && wget https://github.com/seqan/seqan/archive/seqan-v2.4.0.tar.gz && \
  tar xvzf seqan-v2.4.0.tar.gz && \
  cd seqan-seqan-v2.4.0 && \
  mkdir -p build  &&  \
  cd build && \
  cmake .. && \
  make fiona && \
  make compute_gain && \
  cp bin/fiona /usr/local/bin/ && \
  cp bin/compute_gain /usr/local/bin/ && \
  cd /work && rm -rf seqan-seqan-v2.4.0 seqan-seqan-v2.4.0.tar.gz

ENV RUN_CMD fiona

