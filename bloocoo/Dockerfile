FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
    git clone --recursive https://github.com/GATB/bloocoo.git && \
    cd bloocoo && \
    # Prepare GATB sub-module
    git submodule init && \
    git submodule update && \
    # Prepare directories:
    rm -rf build && \
    mkdir  build && \
    # Go in the 'build' directory
    cd build && \
    # Prepare the makefile
    cmake .. && \
    # Run the newly created makefile:
    make -j8


RUN cd /work && cp bloocoo/build/bin/Bloocoo /usr/local/bin

ENV RUN_CMD Bloocoo

