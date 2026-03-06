FROM ghcr.io/nelhage/llama AS llama

# Build stage: compile GCC 15.2.0 from source
FROM ubuntu:noble AS gcc-builder
RUN apt-get update && apt-get -y install \
    gcc g++ make wget xz-utils \
    libgmp-dev libmpfr-dev libmpc-dev \
    zlib1g-dev && \
    apt-get clean

ARG GCC_VERSION=15.2.0
RUN wget -q https://ftp.gnu.org/gnu/gcc/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.xz && \
    tar xf gcc-${GCC_VERSION}.tar.xz && \
    cd gcc-${GCC_VERSION} && \
    contrib/download_prerequisites && \
    mkdir build && cd build && \
    ../configure \
        --prefix=/opt/gcc-${GCC_VERSION} \
        --enable-languages=c,c++ \
        --disable-multilib \
        --disable-bootstrap \
        --with-system-zlib && \
    make -j$(nproc) && \
    make install

# Final image
FROM ubuntu:noble
RUN apt-get update && apt-get -y install ca-certificates && apt-get clean
COPY --from=gcc-builder /opt/gcc-15.2.0 /opt/gcc-15.2.0
RUN echo /opt/gcc-15.2.0/lib64 > /etc/ld.so.conf.d/gcc-15.conf && ldconfig
ENV PATH=/opt/gcc-15.2.0/bin:$PATH
COPY --from=llama /llama_runtime /llama_runtime
WORKDIR /
ENTRYPOINT ["/llama_runtime"]
