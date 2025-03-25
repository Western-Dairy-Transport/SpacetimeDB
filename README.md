<p align="center">
    <a href="https://spacetimedb.com#gh-dark-mode-only" target="_blank">
	<img width="320" src="./images/dark/logo.svg" alt="SpacetimeDB Logo">
    </a>
    <a href="https://spacetimedb.com#gh-light-mode-only" target="_blank">
	<img width="320" src="./images/light/logo.svg" alt="SpacetimeDB Logo">
    </a>
</p>
<p align="center">
    <a href="https://spacetimedb.com#gh-dark-mode-only" target="_blank">
        <img width="250" src="./images/dark/logo-text.svg" alt="SpacetimeDB">
    </a>
    <a href="https://spacetimedb.com#gh-light-mode-only" target="_blank">
        <img width="250" src="./images/light/logo-text.svg" alt="SpacetimeDB">
    </a>
    <h3 align="center">
        'Multiplayer' web apps, at the speed of light.
    </h3>
</p>
<p align="center">
    <a href="https://github.com/clockworklabs/spacetimedb"><img src="https://img.shields.io/github/v/release/clockworklabs/spacetimedb?color=%23ff00a0&include_prereleases&label=version&sort=semver&style=flat-square"></a>
    &nbsp;
    <a href="https://github.com/clockworklabs/spacetimedb"><img src="https://img.shields.io/badge/built_with-Rust-dca282.svg?style=flat-square"></a>
    &nbsp;
	<a href="https://github.com/clockworklabs/spacetimedb/actions"><img src="https://img.shields.io/github/actions/workflow/status/clockworklabs/spacetimedb/ci.yml?style=flat-square&branch=master"></a>
    &nbsp;
    <a href="https://status.spacetimedb.com"><img src="https://img.shields.io/uptimerobot/ratio/7/m784409192-e472ca350bb615372ededed7?label=cloud%20uptime&style=flat-square"></a>
    &nbsp;
    <a href="https://hub.docker.com/r/clockworklabs/spacetimedb"><img src="https://img.shields.io/docker/pulls/clockworklabs/spacetimedb?style=flat-square"></a>
    &nbsp;
    <a href="https://github.com/clockworklabs/spacetimedb/blob/master/LICENSE.txt"><img src="https://img.shields.io/badge/license-BSL_1.1-00bfff.svg?style=flat-square"></a>
</p>
<br>

## What is [SpacetimeDB](https://spacetimedb.com)?

You can think of SpacetimeDB as both a database and server combined into one.

A relational database system placing application logic directly in the database via fancy stored procedures called "modules."

Instead of deploying a web server that sits in between your clients and your database, your clients connect directly to the database and execute your application logic *inside* the database itself. You can write all your RBAC / auth logic right inside your module just like in a normal server.

This means that you can write your entire app in a single language, Rust, and deploy it as a single binary. No more microservices, no more containers, no more Kubernetes, Docker, VMs, goodbye DevOps, infrastructure, ops... no more "servers."

<figure>
    <img src="./images/basic-architecture-diagram.png" alt="SpacetimeDB Architecture" style="width:100%">
    <figcaption align="center">
        <p align="center"><b>SpacetimeDB application architecture</b><br /><sup><sub>(elements in white are provided by SpacetimeDB)</sub></sup></p>
    </figcaption>
</figure>

SpacetimeDB is a database that's orders of magnitude faster than any smart contract system.

So fast, in fact, that the entire backend of the MMORPG [BitCraft Online](https://bitcraftonline.com) is just a SpacetimeDB module. They don't have any other servers or services running, which means that everything in the game- all of the chat messages, items, resources, terrain- even the locations of players, are stored and processed by the database before being synchronized out to all of the clients **in *real-time***.

SpacetimeDB designed and optimized for maximum speed / minimum latency in real-time web apps and collaboration tools, rather than OLAP / batch processing. This speed and latency is achieved by holding the full application state *in-memory*, while persisting data in a write-ahead-log (WAL).

## Installation

Run SpacetimeDB as a standalone database server via the `spacetime` CLI.
[Install](https://spacetimedb.com/install) instructions are outlined below:

#### macOS

Installing on macOS is as simple as running our install script. After that you can use the spacetime command to manage versions.

```bash
curl -sSf https://install.spacetimedb.com | sh
```

#### Linux

Installing on Linux is as simple as running our install script. After that you can use the spacetime command to manage versions.

```bash
curl -sSf https://install.spacetimedb.com | sh
```

#### Windows

Installing on Windows is as simple as pasting this snippet below into PowerShell. To use it in WSL, follow the above Linux instructions instead.

```ps1
iwr https://windows.spacetimedb.com -useb | iex
```

#### Installing from Source

A quick note on installing from source: we recommend that you don't install from source unless there is a feature that is available in `master` that hasn't been released yet, otherwise follow the official installation instructions.

##### MacOS + Linux

Installing on macOS + Linux is pretty straightforward. First we are going to build all of the binaries that we need:

```bash
# Install rustup, you can skip this step if you have cargo and the wasm32-unknown-unknown target already installed.
curl https://sh.rustup.rs -sSf | sh
# Clone SpacetimeDB
git clone https://github.com/clockworklabs/SpacetimeDB
# Build and install the CLI
cd SpacetimeDB
cargo build --locked --release -p spacetimedb-standalone -p spacetimedb-update -p spacetimedb-cli

# Create directories
mkdir -p ~/.local/bin
export STDB_VERSION="$(./target/release/spacetimedb-cli --version | sed -n 's/.*spacetimedb tool version \([0-9.]*\);.*/\1/p')"
mkdir -p ~/.local/share/spacetime/bin/$STDB_VERSION

# Install the update binary
cp target/release/spacetimedb-update ~/.local/bin/spacetime
cp target/release/spacetimedb-cli ~/.local/share/spacetime/bin/$STDB_VERSION
cp target/release/spacetimedb-standalone ~/.local/share/spacetime/bin/$STDB_VERSION
```

At this stage you'll need to add ~/.local/bin to your path if you haven't already.

```
# Please add the following line to your shell configuration and open a new shell session:
export PATH="$HOME/.local/bin:$PATH"

```

Then finally set your SpacetimeDB version:
```

# Then, in a new shell, set the current version:
spacetime version use $STDB_VERSION

# If STDB_VERSION is not set anymore then you can use the following command to list your versions:
spacetime version list
```

You can verify that the correct version has been installed via `spacetime --version`.

#### Running with Docker

You can run Spacetime in a container, using the following command to start a new instance:

```bash
docker run --rm --pull always -p 3000:3000 clockworklabs/spacetime start
```

## Documentation

For more information about SpacetimeDB, getting started guides, game development guides, and reference material please see our [documentation](https://spacetimedb.com/docs).

## Quick Start Guides

There's several getting started guides for each of their supported languages to help you get up and running with SpacetimeDB, on the [docs page](https://spacetimedb.com/docs).

**TL;DR** In summary there are only 4 steps to getting started with SpacetimeDB.

1. Install the `spacetime` CLI.
2. Start a SpacetimeDB node via `spacetime start`.
3. Write and upload a module in one of the supported module languages, either `Rust` or `C#` (more in development)
4. Connect to the database with a client library.

Supported languages and their quick start guides can be found below:

#### Serverside Libraries

- [Rust](https://spacetimedb.com/docs/modules/rust/quickstart)
- [C#](https://spacetimedb.com/docs/modules/c-sharp/quickstart)

#### Client Libraries

- [Rust](https://spacetimedb.com/docs/sdks/rust/quickstart)
- [C#](https://spacetimedb.com/docs/sdks/c-sharp/quickstart)
- [Typescript](https://spacetimedb.com/docs/sdks/typescript/quickstart)


## License

"SpacetimeDB is licensed under BSL 1.1, and in a few years will convert to AGPL v3.0 with a custom linking exception. Our motivation for choosing a free software license is to ensure that contributions made to SpacetimeDB are propagated back to the community. We are expressly not interested in forcing users of SpacetimeDB to open source their own code if they link with SpacetimeDB, so we needed to include a linking exception."
