# NX709J Ubuntu Touch kernel

This repository contains the Linux 5.10.66 ARM64 kernel source for the RedMagic 7 Pro (NX709J), based on Android Common Kernel. It is configured for GSI and Ubuntu Touch use.

## Device and Halium changes

- Added `arch/arm64/configs/nx709j_defconfig`, captured from the working NX709J kernel.
- Extended `arch/arm64/configs/halium.config` with SPI memory and USB UVC support, UBSAN array-bounds settings, and the namespaces, virtual terminal, and file-handle options used by Halium userspace.

## Build

Build on a Linux x86_64 host with Make, Python 3, Flex, Bison, `bc`, OpenSSL development files, and the AArch64 cross tools available. Use Android's clang/LLD 12 toolchain (the config was checked with clang 12.0.5 / LLD 12.0.5). Put the toolchain's `bin` directory and the AArch64 cross tools on `PATH`.

For example, after setting `PATH` for those tools:

```sh
make O=out ARCH=arm64 LLVM=1 LLVM_IAS=1 CROSS_COMPILE=aarch64-linux-gnu- nx709j_defconfig
make O=out ARCH=arm64 LLVM=1 LLVM_IAS=1 CROSS_COMPILE=aarch64-linux-gnu- -j"$(nproc)" Image
```

The resulting uncompressed ARM64 kernel image is `out/arch/arm64/boot/Image`. The supplied defconfig is based on the config embedded in the working NX709J kernel. Kconfig may refresh compiler capability fields when a different toolchain is used.

## License

The kernel source is distributed under the licenses in `COPYING` and `LICENSES/`. Individual files may have additional license terms.
