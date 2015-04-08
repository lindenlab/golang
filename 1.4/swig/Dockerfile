FROM registry.docker/golang

RUN apt-get update && apt-get install -y \
            --no-install-recommends \
            build-essential \
            libpcre3-dev \
            openssl \
            libssl-dev \
            libncurses5 \
            libncurses5-dev \
            uuid \
            uuid-dev 

RUN mkdir /src && cd /src && wget http://sourceforge.net/projects/swig/files/swig/swig-3.0.5/swig-3.0.5.tar.gz && \
	tar -xvf swig-3.0.5.tar.gz && cd swig-3.0.5 && ./configure && make && make install
