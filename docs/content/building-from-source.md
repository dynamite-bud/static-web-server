# Building from Source

Follow these instructions to either build **`SWS`** project from the source or the HTML documentation.

## Building project from source

If you want to build **SWS** from the source, all you need is a [Rust 2021 Edition](https://blog.rust-lang.org/2021/05/11/edition-2021.html) installed.

So make sure to install Rust [1.66.0](https://blog.rust-lang.org/2022/12/15/Rust-1.66.0.html) or higher (or nightly) along with [the toolchain(s)](https://rust-lang.github.io/rustup/concepts/toolchains.html) of your preference.

Then clone the repository and use [Cargo](https://doc.rust-lang.org/cargo/) to build the project from the source.

```sh
git clone https://github.com/static-web-server/static-web-server.git
cd static-web-server
cargo build --release
```

Finally, the release binary should be available at `target/release/static-web-server` or under your toolchain directory chosen.

!!! info "Don't use the project's `Makefile`"
    Please don't use the project's `Makefile` since it's only intended for development and some on-demand tasks.

## Building documentation from source

All HTML documentation is located in the `docs/` project's directory and is built using [Material for MkDocs](https://github.com/squidfunk/mkdocs-material).

It's only necessary to have [Docker](https://www.docker.com/get-started/) installed.

## Cargo features

Some features are optional when running or building from the source.
For example, if you want to run without the default features like `http2` just try.

```sh
cargo run --no-default-features -- -h
```

For more optional features take a look a the `[features]` section of the `cargo.toml` file adjusting them on demand.

### Building documentation

By default the docs will be built in the `/tmp/docs` directory, to do so follow these steps.

```sh
git clone https://github.com/static-web-server/static-web-server.git
cd static-web-server
mkdir /tmp/docs
docker run -it --rm \
    -v $PWD/docs:/docs \
    -v /tmp/docs:/tmp/docs squidfunk/mkdocs-material build
```

!!! tip "Output the docs in a different directory"
    If you want to output the docs in a different directory then append the `--site-dir=/new/dir/path/` argument to the *"squidfunk/mkdocs-material"* `build` command and make sure to provide the new directory path.

### Development server

If you want to improve the documentation then run the built-in development server via `docs/docker-compose.yml`.

```sh
git clone https://github.com/static-web-server/static-web-server.git
cd static-web-server
docker-compose -f docs/docker-compose.yml up
```

Now the server will be available at `localhost:8000`