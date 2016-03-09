FROM registry.docker/golang:1.6.0

RUN apt-get update && apt-get install -y \
            --no-install-recommends \
            autogen \
            autoconf \
            automake \
            bison \
            build-essential \
            libpcre3-dev \
            openssl \
            libssl-dev \
            libncurses5 \
            libncurses5-dev \
            uuid \
            uuid-dev 

RUN mkdir /src
COPY swig-3.0.8.tar.gz /src/
RUN cd /src && tar -xvf swig-3.0.8.tar.gz && cd swig-3.0.8 && \
    ./autogen.sh && ./configure --prefix=/usr && make && \
    make install-main && make install-lib && rm -rf /src
