FROM rcents/im:base

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

RUN apt-get update -y && \
    apt-get install -y libboost-all-dev;

RUN cd /work && \
    wget http://www.cbcb.umd.edu/software/quake/downloads/quake-0.3.5.tar.gz && \
    tar -xzf quake-0.3.5.tar.gz && \
    rm quake-0.3.5.tar.gz && \
    cd Quake/src && \
    sed -i '/CFLAGS=-O3 -fopenmp -I\/opt\/local\/var\/macports\/software\/boost\/1.46.1_0\/opt\/local\/include -I./c\CFLAGS=-O3 -fopenmp -fpermissive -std=gnu++98 -I\/usr\/include -I.' Makefile && \
    echo -e "install:all\n\tcp \$(EXE_FILES) *.a /usr/bin/"  >> Makefile && \
    make && \
    make install && \
    cd ../bin && \
    cp *.py *.r /usr/bin/  

RUN cd work && wget https://github.com/gmarcais/Jellyfish/releases/download/v1.1.12/jellyfish-1.1.12.tar.gz && \
    tar -xvzf jellyfish-1.1.12.tar.gz && \
    rm jellyfish-1.1.12.tar.gz && \
    cd jellyfish-1.1.12 && \
    ./configure --prefix=/usr/ && \
    make && \
    make install 

RUN echo deb http://mirror.las.iastate.edu/CRAN/bin/linux/debian stretch-cran35/ >> /etc/apt/sources.list && \
    apt-get -y update && \
    apt-key adv --keyserver keys.gnupg.net --recv-key "E19F5F87128899B192B1A2C2AD5F960A256A04AF" && \
    apt-get -y update && \
    apt-get install -y r-base r-base-dev

RUN R -e "install.packages('VGAM', repos='https://cloud.r-project.org' )"


ENV RUN_CMD quake.py
