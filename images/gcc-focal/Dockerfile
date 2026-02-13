FROM ghcr.io/jiayuehua/llama as llama
FROM ubuntu:noble
RUN apt-get update && apt-get -y install gcc g++ gcc-13 g++-13 ca-certificates && apt-get clean
COPY --from=llama /llama_runtime /llama_runtime
WORKDIR /
ENTRYPOINT ["/llama_runtime"]
