# wolfboot-ci-renode: Renode emulation environment for wolfBoot CI
FROM antmicro/renode:latest

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc-arm-none-eabi \
    make \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

RUN mkdir -p /tmp/test_results/

WORKDIR /workspace
