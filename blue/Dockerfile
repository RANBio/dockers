FROM rcents/im:base

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF; \
  echo "deb http://download.mono-project.com/repo/debian stable-stretch main" > /etc/apt/sources.list.d/mono-official-stable.list; \
  apt-get update


RUN set ex; \
  apt-get update -y; \
  apt-get install -y --no-install-recommends \
  mono-complete

RUN wget https://bioinformatics.csiro.au/public/files/Linux-1.1.3.tar.gz; \
  tar xvzf Linux-1.1.3.tar.gz; \
  mv Linux/* .
