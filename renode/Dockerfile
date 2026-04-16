# wolfboot-ci-renode: Renode emulation environment for wolfBoot CI
ARG BASE_TAG=latest
FROM antmicro/renode:latest AS renode-src

ARG BASE_TAG=latest
FROM ghcr.io/wolfssl/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc-arm-none-eabi \
    binutils-arm-none-eabi \
    libstdc++-arm-none-eabi-dev \
    libstdc++-arm-none-eabi-newlib \
    gcc-multilib \
    libc6-dev-i386 \
    libicu-dev \
    make \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Install .NET 8 runtime (required by Renode >= 1.16)
RUN curl -sSL https://dot.net/v1/dotnet-install.sh -o /tmp/dotnet-install.sh \
    && chmod +x /tmp/dotnet-install.sh \
    && /tmp/dotnet-install.sh --channel 8.0 --runtime dotnet --install-dir /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm /tmp/dotnet-install.sh

COPY --from=renode-src /opt/renode /opt/renode

ENV PATH="/opt/renode:${PATH}"
RUN ln -s /opt/renode/renode /usr/bin/renode \
    && chmod +x /opt/renode/renode \
    && mkdir -p /tmp/test_results

WORKDIR /workspace
