FROM ghcr.io/nelhage/llama AS llama

FROM ubuntu:noble
RUN apt-get update && \
    apt-get -y install --no-install-recommends software-properties-common ca-certificates && \
    add-apt-repository ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get -y install --no-install-recommends gcc-15 g++-15 && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-15 100 \
                        --slave /usr/bin/g++ g++ /usr/bin/g++-15 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
COPY --from=llama /llama_runtime /llama_runtime
WORKDIR /
ENTRYPOINT ["/llama_runtime"]
