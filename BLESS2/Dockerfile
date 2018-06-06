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

RUN apt-get update -y && apt-get install -y mpich libboost-all-dev libbz2-dev

RUN cd /work && \
    wget https://downloads.sourceforge.net/project/bless-ec/bless.v1p02.tgz && \
    tar xvzf bless.v1p02.tgz && \
    cd v1p02 &&  \
    sed -i 's/DISABLE_ASMLIB = false/DISABLE_ASMLIB = true/' kmc/makefile && \
    sed -i 's/\$(KMC_MAIN_DIR)\/libs\/libz.a/ -lz /' kmc/makefile && \
    sed -i 's/\$(KMC_MAIN_DIR)\/libs\/libbz2.a/ -lbz2 /' kmc/makefile && \
    sed -i 's/CFLAGS=.*/CFLAGS=-Wall -O -I \/usr\/include -I klib\/ -I google-sparsehash\/ -I kmc\/kmc_api\/ -fopenmp -std=c++11/' Makefile && \
    sed -i 's/LDFLAGS=.*/LDFLAGS=-lboost_filesystem -lboost_system -lboost_iostreams -lz -fopenmp -std=c++11/' Makefile && \
    make && \
    cp bless /usr/local/bin && \
    cp kmc/bin/kmc /usr/local/bin 

ENV RUN_CMD bless
