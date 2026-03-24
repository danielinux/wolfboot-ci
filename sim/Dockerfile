# wolfboot-ci-sim: Host simulator environment for wolfBoot CI
ARG BASE_TAG=latest
FROM ghcr.io/danielinux/wolfboot-ci-base:${BASE_TAG}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    libc6-dev-i386 \
    check \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /workspace
