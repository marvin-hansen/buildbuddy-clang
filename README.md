# buildbuddy-clang

Minified Clang toolchain distribution 

### About

This repository contains Github Actions to build and package Rust and C toolchains for consumption with Bazel and
optimized for buildbuddy CI.

#### Rust

Currently we just re-compress the Rust toolchains from `static.rust-lang.org` with [`zstd`](https://github.com/facebook/zstd)
which has much faster decompression times than the default `LZMA2` algorithm typically used with `.tar.xz` package.

#### C (Clang)

We build a Clang toolchain from the upstream source [`llvm-project`](https://github.com/llvm/llvm-project) with CMake and Ninja. 
Generally following the instructions from:

* [Clang - Getting Started](https://clang.llvm.org/get_started.html)
* [Building LLVM with CMake](https://llvm.org/docs/CMake.html)
* [Assembling a Complete Toolchain](https://clang.llvm.org/docs/Toolchain.html)

The resulting toolchain is designed for consumption with [`toolchains_llvm`](https://github.com/bazel-contrib/toolchains_llvm)
and to be a drop-in replacement for the toolchains provided by the upstream `llvm-project`. Similar to Rust, we also compress
the package with `zstd`.

## Acknowledgements

This repo started out as a fork from https://github.com/MaterializeInc/toolchains

Special thanks to [@Parker](https://github.com/ParkMyCar) for open sourcing and maintaining the said repo. 

Also, special thanks to [@scasagrande ](https://github.com/scasagrande)for his work on [sysroot building for llvm toolchain.](https://github.com/scasagrande/toolchains_llvm_sysroot) 

## License

Apache-2.0, as the original repo.