# Light Firmware

A simple light firmware implemented using the
[tosca](https://github.com/ToscaLab/tosca) framework for OS-based systems.

## Building

```console
cargo build [--release]
```

To build a firmware for `Linux` systems with the `musl` target:

```console
cargo build [--release] --target x86_64-unknown-linux-musl
```

The `--release` option configures the build to use the `release` profile,
enabling all time and memory optimizations for the target architecture.

## Cross-compilation for `aarch64` architecture (ARM64)

Install the [cross](https://github.com/cross-rs/cross) binary, which allows you
to easily cross-compile Rust projects using Docker, without the need to manage
custom `Dockerfile`s.

```console
cargo install -f cross --git https://github.com/cross-rs/cross
```

The `git` option allows you to use the latest `docker` images. Although the
`cross` project is actively maintained, it doesn't release frequently, so
published versions can quickly become outdated.

To build a firmware for `Linux` systems running on `ARM64` architecture:

```console
cross build [--release] --target=aarch64-unknown-linux-gnu
```

To build a firmware with the `musl` library for `Linux` systems running on
`ARM64` architecture:

```console
cross build [--release] --target=aarch64-unknown-linux-musl
```

The `--release` option configures the build with the Rust `release` profile,
enabling all time and memory optimizations for the `ARM64` architecture.

## Running the server

The firmware is a server that runs on `localhost` and listens on port `3000` by
default.
To start the server, you must provide the `hostname` and the discovery process
`domain` as input.

```console
cargo run -- --hostname HOSTNAME --domain DOMAIN
```

where `HOSTNAME` refers to the chosen server hostname, and `DOMAIN` represents
the domain sought by a client during the network discovery process.

At server startup, an initial message is printed to signal its successful
execution.

```
Starting server...
```
