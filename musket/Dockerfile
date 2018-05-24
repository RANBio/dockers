FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin;

  
RUN wget https://downloads.sourceforge.net/project/musket/musket-1.1.tar.gz && \
    tar -xzvf musket-1.1.tar.gz && \
    cd musket-1.1 && \
    make && \
    cp musket /usr/local/bin