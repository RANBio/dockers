FROM rcents/im:base

ENV WORK /work

RUN cd /work && wget https://www.cs.helsinki.fi/u/lmsalmel/coral/coral-1.4.1.tar.gz && \
    tar -xzvf coral-1.4.1.tar.gz  && \
    cd coral-1.4.1/ && \
    make && \
    cp coral /usr/local/bin

ENV RUN_CMD coral
