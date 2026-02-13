FROM ghcr.io/nelhage/llama as llama
FROM ubuntu:noble
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -y install \
        lsb-release wget software-properties-common valgrind zlib1g-dev
ADD https://apt.llvm.org/llvm.sh /tmp/llvm.sh
RUN bash /tmp/llvm.sh 20 
RUN update-alternatives --install /usr/bin/cc cc /usr/bin/clang-20 200 && \
    update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++-20 200
COPY --from=llama /llama_runtime /llama_runtime
WORKDIR /
ENTRYPOINT ["/llama_runtime"]
