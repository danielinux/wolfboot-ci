# wolfBoot CI Container Images

Pre-built Docker images for wolfBoot GitHub Actions CI, eliminating per-run
toolchain downloads and apt-get overhead.

## Images

All images use Devuan testing as the base (except renode).

| Image | Purpose | Base |
|-------|---------|------|
| `wolfboot-ci-base` | Shared foundation: build-essential, cmake, ninja, python3, libwolfssl-dev | devuan:testing |
| `wolfboot-ci-arm` | ARM cross-compilation: arm-none-eabi-gcc, aarch64-linux-gnu, clang | base |
| `wolfboot-ci-powerpc` | PowerPC cross-compilation: powerpc-linux-gnu-gcc | base |
| `wolfboot-ci-sim` | Host simulator tests: 32-bit libc, libcheck | base |
| `wolfboot-ci-m33mu` | TrustZone emulator tests: ARM toolchain + m33mu | devuan:testing |
| `wolfboot-ci-riscv` | RISC-V: xPack GCC + freedom-e-sdk | base |
| `wolfboot-ci-aarch64` | Bare-metal AArch64: aarch64-none-elf toolchain | base |
| `wolfboot-ci-x86` | x86 QEMU: nasm, gcc-multilib, qemu-system-x86, swtpm | base |
| `wolfboot-ci-renode` | Renode emulation: renode + arm-none-eabi-gcc | antmicro/renode |

## Building locally

```bash
# Build base first
podman build --no-cache -t wolfboot-ci-base:testing base/

# Build derived images (replace 'arm' with any image name)
podman build --no-cache --build-arg BASE_TAG=testing -t wolfboot-ci-arm:testing arm/

# Build m33mu image
podman build --no-cache -t wolfboot-ci-m33mu:testing m33mu/
```

## Usage in GitHub Actions

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/wolfssl/wolfboot-ci-arm:latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true
      - name: Init submodules
        run: |
          git config --global --add safe.directory "$GITHUB_WORKSPACE"
          git submodule update --init --single-branch
      - name: Build
        run: make
```

## Publishing

Images are automatically built and published to GHCR when a version tag is pushed:

```bash
git tag v1.0
git push origin v1.0
```

Individual images can also be built via workflow dispatch.
