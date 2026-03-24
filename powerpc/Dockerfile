# wolfboot-ci-powerpc: PowerPC cross-compilation for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/wolfssl/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc-powerpc-linux-gnu \
    libc6-dev-powerpc-cross \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /workspace
