FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin

RUN wget http://packages.seqan.de/fiona/fiona-0.2.10-Linux-x86_64.tar.xz && \
  tar -xf fiona-0.2.10-Linux-x86_64.tar.xz && \
  cd fiona-0.2.10-Linux-x86_64/bin && \
  cp fiona /usr/local/bin;