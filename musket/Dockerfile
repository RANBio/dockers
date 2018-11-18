FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin && \
  cd /work && rm -rf bwa

  
RUN cd /work/ && wget https://downloads.sourceforge.net/project/musket/musket-1.1.tar.gz && \
    tar -xzvf musket-1.1.tar.gz && \
    cd musket-1.1 && \
    make && \
    cp musket /usr/local/bin && \
    cd ../ && rm -rf musket-1.1

RUN apt-get update && apt-get install -y mpich

RUN pip install numpy && \
    pip install mpi4py

RUN cd /work && \
  git clone https://github.com/srirampc/ecet.git && \
  cd /work/ecet && \
  make ecet && \
  cp bin/* /usr/local/bin/ && \
  rm -rf /work/ecet


ENV RUN_CMD musket

