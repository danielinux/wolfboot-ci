# wolfboot-ci-aarch64: Bare-metal AArch64 cross-compilation for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/danielinux/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

# ARM GNU Toolchain for aarch64-none-elf (bare-metal)
ARG ARM_GCC_VERSION=14.3.rel1
ARG ARM_GCC_TARBALL=arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-elf.tar.xz

RUN set -eux; \
    cd /tmp; \
    wget -q "https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu/${ARM_GCC_VERSION}/binrel/${ARM_GCC_TARBALL}"; \
    mkdir -p /opt; \
    tar -C /opt -xf "${ARM_GCC_TARBALL}"; \
    rm -f "${ARM_GCC_TARBALL}"

ENV PATH="/opt/arm-gnu-toolchain-${ARM_GCC_VERSION}-x86_64-aarch64-none-elf/bin:${PATH}"

WORKDIR /workspace
