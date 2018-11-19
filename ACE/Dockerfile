FROM rcents/im:base

ENV WORK /work


RUN cd /work && \
    git clone https://github.com/Sheikhizadeh/ACE.git && \
    cd ACE && \
    wget https://raw.githubusercontent.com/RCENTS/containers/master/ACE/ace.patch -O ace.patch && \
    git apply ace.patch && \
    make && \
    cp ace /usr/local/bin

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

RUN cd /work && \
   git clone https://github.com/lucian-ilie/Correcting-Illumina-data.git && \
   cd /work/Correcting-Illumina-data/readSearch && \
   make && \
   cp readSearch /usr/local/bin && \
   cd /work/Correcting-Illumina-data/kmerSearch && \
   make && \
   cp kmerSearch /usr/local/bin

ENV RUN_CMD ace
