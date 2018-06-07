FROM registry.docker/buildpack-deps:jessie-scm

# gcc for cgo
# apparmer, iptables, libltdl7
RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
		libapparmor1 \
		iptables \
		libltdl7 \
		pkg-config \
	&& rm -rf /var/lib/apt/lists/*

# pinned to linden/jenkins built docker
RUN curl -k https://int.infra-jenkins.build.sansar.io/job/build-package-docker-engine-1.12/lastSuccessfulBuild/artifact/repo/docker-engine_1.12.6~linden1-0~debian-jessie_amd64.deb -o docker-engine_1.12.6~linden1-0~debian-jessie_amd64.deb \
    && dpkg -i docker-engine_1.12.6~linden1-0~debian-jessie_amd64.deb \
    && rm docker-engine_1.12.6~linden1-0~debian-jessie_amd64.deb

ENV GOLANG_VERSION 1.7.5
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 2e4dd6c44f0693bef4e7b46cc701513d74c3cc44f2419bf519d7868b12931ac3

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
