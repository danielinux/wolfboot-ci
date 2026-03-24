# m33mu-ci: Devuan testing CI image for Zephyr + m33mu
FROM docker.io/devuan/devuan:testing

ENV DEBIAN_FRONTEND=noninteractive

# ---- Base build tooling + deps (as provided) ----
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl wget xz-utils file \
    git build-essential pkg-config \
    cmake ninja-build \
    python3 python3-pip python3-venv python3-full \
    gcc-arm-none-eabi \
    binutils-arm-none-eabi \
    libstdc++-arm-none-eabi-dev \
    libstdc++-arm-none-eabi-newlib \
    gdb-multiarch \
    libtpms-dev vde2 \
    libcapstone-dev \
    libwolfssl-dev \
    libvdeplug-dev \
    vde-switch \
    libdw-dev libelf-dev \
    libncurses-dev \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# ---- Zephyr SDK ----
#ARG ZEPHYR_SDK_VERSION=0.17.4
#ARG ZEPHYR_SDK_ARCH=linux-x86_64
#
#RUN set -eux; \
#    cd /tmp; \
#    wget -q "https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v${ZEPHYR_SDK_VERSION}/zephyr-sdk-${ZEPHYR_SDK_VERSION}_${ZEPHYR_SDK_ARCH}.tar.xz"; \
#    wget -q "https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v${ZEPHYR_SDK_VERSION}/sha256.sum"; \
#    grep "zephyr-sdk-${ZEPHYR_SDK_VERSION}_${ZEPHYR_SDK_ARCH}.tar.xz" sha256.sum | sha256sum -c -; \
#    mkdir -p /opt; \
#    tar -C /opt -xf "zephyr-sdk-${ZEPHYR_SDK_VERSION}_${ZEPHYR_SDK_ARCH}.tar.xz"; \
#    rm -f "zephyr-sdk-${ZEPHYR_SDK_VERSION}_${ZEPHYR_SDK_ARCH}.tar.xz" sha256.sum
#
#ENV ZEPHYR_TOOLCHAIN_VARIANT=zephyr
#ENV ZEPHYR_SDK_INSTALL_DIR=/opt/zephyr-sdk-${ZEPHYR_SDK_VERSION}
#
## ---- Python venv for west (avoids PEP 668 externally-managed-environment) ----
#ENV VIRTUAL_ENV=/opt/venv
#ENV PATH="${VIRTUAL_ENV}/bin:${PATH}"
#
#RUN python3 -m venv "${VIRTUAL_ENV}" \
# && "${VIRTUAL_ENV}/bin/pip" install --no-cache-dir --upgrade pip setuptools wheel \
# && "${VIRTUAL_ENV}/bin/pip" install --no-cache-dir west


# ---- m33mu: clone, build, install ----
RUN set -eux; \
    git clone --depth 1 https://github.com/danielinux/m33mu.git /tmp/m33mu; \
    cmake -S /tmp/m33mu -B /tmp/m33mu/build; \
    cmake --build /tmp/m33mu/build -j"$(nproc)"; \
    if [ -f /tmp/m33mu/build/m33mu ]; then \
      install -m 0755 /tmp/m33mu/build/m33mu /usr/local/bin/m33mu; \
    fi; \
    rm -rf /tmp/m33mu

WORKDIR /workspace
