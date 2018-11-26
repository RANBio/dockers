FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
  git clone https://github.com/lh3/bwa.git && \
  cd /work/bwa && \
  make && \
  cp bwa /usr/local/bin && \
  rm -rf /work/bwa

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
  cp bowtie2* /usr/local/bin && \
  rm -rf /work/bowtie2

RUN apt-get update -y && apt-get install -y mpich 
RUN update-alternatives --set mpi /usr/include/mpich
RUN update-alternatives --set mpirun /usr/bin/mpirun.mpich

RUN apt-get update -y && apt-get install -y libboost-all-dev libbz2-dev

RUN apt-get update -y && apt-get install -y swig cpanminus bioperl

RUN cd /work && \
    wget https://downloads.sourceforge.net/project/bless-ec/bless.v1p02.tgz && \
    tar xvzf bless.v1p02.tgz && \
    cd v1p02 &&  \
    wget https://raw.githubusercontent.com/RCENTS/containers/master/BLESS2/bless.patch -O bless.patch && \
    wget https://raw.githubusercontent.com/RCENTS/containers/master/BLESS2/kmc.patch -O kmc.patch && \
    patch Makefile bless.patch && \
    patch kmc/makefile kmc.patch && \
    make && \
    cp bless /usr/local/bin && \
    cp kmc/bin/kmc /usr/local/bin 


RUN cd /work && \
    wget https://github.com/broadinstitute/picard/releases/download/2.18.17/picard.jar && \
    mv picard.jar /usr/local/bin && \
    echo "#!/bin/bash" > /usr/local/bin/picard.sh && \
    echo "java -Xmx2g -jar /usr/local/bin/picard.jar \"\$\@\" " >> /usr/local/bin/picard.sh && \
    chmod a+x /usr/local/bin/picard.sh

RUN cd /work && \
    wget https://github.com/biod/sambamba/releases/download/v0.6.8/sambamba-0.6.8-linux-static.gz && \
    gunzip -c sambamba-0.6.8-linux-static.gz > sambamba && \
    chmod a+x sambamba && \
    mv sambamba /usr/local/bin/



RUN cpanm https://cpan.metacpan.org/authors/id/M/MK/MKODERER/Sys-CPU-0.52.tar.gz  
RUN cpanm Getopt::Long 
RUN cpanm Compress::Zlib 
RUN cd /work && \
    wget http://www.cpan.org/authors/id/A/AJ/AJGOUGH/Parallel-MPI-Simple-0.10.tar.gz && \
    tar xvzf Parallel-MPI-Simple-0.10.tar.gz && \
    cd Parallel-MPI-Simple-0.10 && \
    perl Makefile.PL LDFLAGS="-lmpich" CCFLAGS="-I/usr/include/mpi" && \
    make && \
    make test && \
    make install

RUN wget https://cpan.metacpan.org/authors/id/L/LD/LDS/Bio-SamTools-1.43.tar.gz  && \
    tar xvzf Bio-SamTools-1.43.tar.gz && \
    cd Bio-SamTools-1.43 && \
    perl INSTALL.pl 

RUN cd /work && \
    wget https://github.com/thirtyeggs/spectacle/archive/0.02.tar.gz -O spectacle-0.02.tar.gz && \
    tar xvzf spectacle-0.02.tar.gz && \
    cd spectacle-0.02 &&  \
    wget https://raw.githubusercontent.com/RCENTS/containers/master/BLESS2/spectacle.patch -O spectacle.patch && \
    patch Makefile spectacle.patch && \
    make && \
    cp bin/* /usr/local/bin/ && \
    cp lib/* /usr/local/lib/

RUN cd /work/ && \
    wget https://github.com/broadinstitute/gatk/releases/download/4.0.11.0/gatk-4.0.11.0.zip && \
    unzip gatk-4.0.11.0.zip && \
    cd gatk-4.0.11.0 && \
    cp gatk /usr/local/bin && \
    cp gatk*.jar /usr/local/bin

ENV RUN_CMD bless
