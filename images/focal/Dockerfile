FROM ghcr.io/jiayuehua/llama as llama
FROM ubuntu:noble
RUN apt-get update && \
        apt-get -y install ca-certificates && \
        apt-get clean
COPY --from=llama /llama_runtime /llama_runtime
ENTRYPOINT ["/llama_runtime"]
