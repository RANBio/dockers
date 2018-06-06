FROM rcents/im:base

ENV WORK /work

RUN cd /work && wget http://mirrors.peers.community/mirrors/gnu/gsl/gsl-latest.tar.gz && \
    tar -zxvf gsl-latest.tar.gz && \
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

ENV RUN_CMD hitec

