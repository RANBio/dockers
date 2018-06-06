FROM rcents/im:base

ENV WORK /work

RUN cd /work && \
    wget "https://sourceforge.net/projects/shrec-ec/files/SHREC 2.2/src.zip" && \
    unzip src.zip && \
    javac *.java 

RUN cd /work/ && \
    echo "Manifest-version: 1.0" > manifest.mf && \
    echo "Main-Class: Shrec" >> manifest.mf && \
    jar cfm shrec.jar manifest.mf *.java *.class && \
    chmod +x shrec.jar && \
    cp shrec.jar /usr/bin/ && \
    echo "#!/bin/bash" > SHREC && \
    echo "echo Arguments \$@" >> SHREC && \
    echo "java -jar /usr/bin/shrec.jar \$@" >> SHREC && \
    chmod +x SHREC && \
    cp SHREC /usr/bin/ 


ENV RUN_CMD SHREC

