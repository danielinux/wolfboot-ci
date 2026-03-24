# wolfboot-ci-riscv: RISC-V cross-compilation for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/wolfssl/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

# xPack RISC-V GCC
ARG RISCV_GCC_VERSION=15.2.0-1
ARG RISCV_GCC_SHA256=aaaa8060c914851a3e5ee1ba82cc3d6f80972f90638a05c6e823a37557a33758

RUN set -eux; \
    cd /tmp; \
    wget -q "https://github.com/xpack-dev-tools/riscv-none-elf-gcc-xpack/releases/download/v${RISCV_GCC_VERSION}/xpack-riscv-none-elf-gcc-${RISCV_GCC_VERSION}-linux-x64.tar.gz"; \
    echo "${RISCV_GCC_SHA256}  xpack-riscv-none-elf-gcc-${RISCV_GCC_VERSION}-linux-x64.tar.gz" | sha256sum -c -; \
    mkdir -p /opt; \
    tar -C /opt -xzf "xpack-riscv-none-elf-gcc-${RISCV_GCC_VERSION}-linux-x64.tar.gz"; \
    rm -f "xpack-riscv-none-elf-gcc-${RISCV_GCC_VERSION}-linux-x64.tar.gz"

ENV PATH="/opt/xpack-riscv-none-elf-gcc-${RISCV_GCC_VERSION}/bin:${PATH}"

# Pre-clone freedom-e-sdk (heavy recursive submodules)
RUN git clone --depth 1 --recursive https://github.com/sifive/freedom-e-sdk.git /opt/freedom-e-sdk

WORKDIR /workspace
