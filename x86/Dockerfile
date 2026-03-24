# wolfboot-ci-x86: x86 QEMU testing environment for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/wolfssl/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    nasm \
    gcc-multilib \
    qemu-system-x86 \
    swtpm \
    uuid-dev \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /workspace
