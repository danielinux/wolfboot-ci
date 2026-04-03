# wolfboot-ci-arm: ARM cross-compilation + clang for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/wolfssl/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc-arm-none-eabi \
    binutils-arm-none-eabi \
    libstdc++-arm-none-eabi-dev \
    libstdc++-arm-none-eabi-newlib \
    gcc-aarch64-linux-gnu \
    libc6-dev-arm64-cross \
    gnu-efi \
    clang llvm lld \
    check \
    cppcheck \
    gdb-multiarch \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /workspace
