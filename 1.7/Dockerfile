FROM registry.docker/buildpack-deps:jessie-scm

# gcc for cgo
RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
		pkg-config \
	&& rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.7.4
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz 
ENV GOLANG_DOWNLOAD_SHA256 4c189111e9ba651a2bb3ee868aa881fab36b2f2da3409e80885ca758a6b614cc

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz && export GOROOT_BOOTSTRAP=/usr/src/go \
	&& ls -l /usr && ls -l / \
	&& cd /usr/local/go/src && ./make.bash --noclean 2>&1

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
