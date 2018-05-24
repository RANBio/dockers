FROM rcents/im:base

ENV WORK /work


RUN cd /work && \
    git clone https://github.com/Sheikhizadeh/ACE.git && \
    cd ACE && \
    sed -i 's/delete prev/delete ::prev/' ace.cpp && \
    sed -i 's/prev=/::prev=/' ace.cpp && \
    sed -i 's/prev\[x\]/::prev\[x\]/' ace.cpp && \
    make && \
    cp ace /usr/local/bin
