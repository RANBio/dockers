FROM rcents/im:base

ENV WORK /work

RUN pip install -U numpy && \
    pip install -U scipy 

RUN cd /work && \
    wget https://downloads.sourceforge.net/project/uc-echo/source%20release/echo_v1_12.tgz && \
    tar xvzf echo_v1_12.tgz && \
    cd echo_v1_12/ && \
    sed -i 's/#include <fcntl.h>/#include <fcntl.h>\n#include <unistd.h>/' MMAP.hpp && \
    echo -e "install:all\n\techo '#!/usr/bin/python' > ECHO.py\n\tcat ErrorCorrection.py >>ECHO.py\n\tchmod 755 \$(TARGETS) ECHO.py\n\tcp \$(TARGETS) ECHO.py /usr/bin/"  >> Makefile && \
    make && \
    make install

ENV RUN_CMD ECHO.py
