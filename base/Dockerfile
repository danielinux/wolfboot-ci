# wolfboot-ci-base: Devuan testing base layer for wolfBoot CI
FROM docker.io/devuan/devuan:testing

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl wget xz-utils file \
    git build-essential pkg-config \
    cmake ninja-build \
    python3 python3-pip python3-venv python3-full python-is-python3 \
    libwolfssl-dev \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /workspace
