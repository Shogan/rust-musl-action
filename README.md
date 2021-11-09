# GitHub Action for Rust and MUSL

Provides a Docker image configuration with pre-installed [osxcross](https://github.com/tpoechtrager/osxcross) for macOS cross compiled / linked builds from debian / ubuntu GitHub actions.

Action provides an environment with stable Rust 1.53, MUSL and the following targets:
- x86_64-unknown-linux-musl
- aarch64-unknown-linux-musl
- x86_64-apple-darwin
- x86_64-pc-windows-gnu

## Usage

To compile a rust binary/library for both `x86_64-apple-darwin` and `x86_64-unknown-linux-musl` targets:

```yaml
name: Rust static build
on:
  push:
    branches:
      - main
jobs:
  build:
    name: build for all platforms
    runs-on: ubuntu-latest
    env:
      CARGO_TERM_COLOR: always
      BINARY_NAME: rust-test1
    steps:
    - uses: actions/checkout@v2
    - name: Build-musl macOS x86
      uses: shogan/rust-musl-action@master
      with:
        args: cargo build --target x86_64-apple-darwin --release
    - name: Build-musl Linux x86
      uses: shogan/rust-musl-action@master
      with:
        args: cargo build --target x86_64-unknown-linux-musl --release
```

## Cargo config

Be sure to add relevant **.cargo/config** configuration to your Rust project in order to specify the linker/target mapping to use for your target(s):

```
[target.x86_64-apple-darwin]
linker = "x86_64-apple-darwin14-clang"
ar = "x86_64-apple-darwin14-ar"
```

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).
