FROM rcents/im:base

ENV WORK /work

RUN cd /work && wget http://mirrors.ocf.berkeley.edu/gnu/gsl/gsl-2.4.tar.gz && \ 
    tar -zxvf gsl-2.4.tar.gz && \
    cd gsl-2.4/ && \
    ./configure --prefix=/usr/ && \
    make && \
    make check && \
    make install;

RUN cd /work && wget http://www.csd.uwo.ca/~ilie/HiTEC/hitec64.tar.gz && \
    tar -xvzf hitec64.tar.gz && \
    cd HiTEC_64bit/ && \
    make && \
    cp hitec /usr/local/bin

RUN cd /work && \
   git clone https://github.com/lucian-ilie/Correcting-Illumina-data.git && \
   cd /work/Correcting-Illumina-data/readSearch && \
   make && \
   cp readSearch /usr/local/bin && \
   cd /work/Correcting-Illumina-data/kmerSearch && \
   make && \
   cp kmerSearch /usr/local/bin 

ADD fq_all2std.pl /usr/local/bin/

ENV RUN_CMD hitec

