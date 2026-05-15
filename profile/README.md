<div align="center">

<img src="./assets/haybarn-icon.png" alt="Haybarn" width="160" />

# Haybarn

**An independent derived distribution of DuckDB.**
*Powered by DuckDB. Published by [Query Farm LLC](https://query.farm).*

<img src="./assets/haybarn-banner.png" alt="A red barn full of hay bales, set against rolling green hills" width="100%" />

</div>

---

## What is Haybarn?

Haybarn is a friendly, independent rebuild of [DuckDB](https://duckdb.org) — branded, signed, and shipped on its own cadence by **Query Farm LLC**. Think of it as the local barn down the road from the duck pond: same grain, different roof.

We rebuild DuckDB from source into our own signed binaries and pair them with a self-contained, signed extension ecosystem. Haybarn stays **ABI-compatible** with upstream DuckDB so forward-porting is cheap and your existing code keeps working.

> *"Haybarn, powered by DuckDB."*

## Why a barn?

Because barns are where you keep what the fields produce — sturdy, dependable, full of useful things stacked neatly out of the rain. That's how we want our distribution to feel.

## What's in here

| Repo | What it is |
| --- | --- |
| [`haybarn`](https://github.com/Query-farm-haybarn/haybarn) | Core fork of DuckDB. The `haybarn` CLI and `libhaybarn`. |
| [`haybarn-python`](https://github.com/Query-farm-haybarn/haybarn-python) | Python bindings — `import haybarn` (or `import haybarn as duckdb`). |
| [`haybarn-iceberg`](https://github.com/Query-farm-haybarn/haybarn-iceberg) | Apache Iceberg extension, rebuilt for Haybarn. |
| [`haybarn-ducklake`](https://github.com/Query-farm-haybarn/haybarn-ducklake) | DuckLake extension, rebuilt for Haybarn. |

Extensions install just like upstream:

```sql
INSTALL iceberg;
LOAD iceberg;
```

…they're served from `haybarn-extensions.query.farm` and signed with the Haybarn extension key.

## Build status

Each row is a Haybarn repo. Each version column shows the CI for builds against that DuckDB base. We straddle versions during a rebase, so expect more than one column to be live at any given time.

| Repo | Latest release | DuckDB **v1.5.2** *(current)* | DuckDB **v1.5.3** *(next)* |
| --- | :---: | :---: | :---: |
| [`haybarn`](https://github.com/Query-farm-haybarn/haybarn) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn/releases) | [![release CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn/haybarn-release.yml?branch=haybarn&label=release)](https://github.com/Query-farm-haybarn/haybarn/actions/workflows/haybarn-release.yml) <br> [![extensions CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn/haybarn-extensions.yml?branch=haybarn&label=extensions)](https://github.com/Query-farm-haybarn/haybarn/actions/workflows/haybarn-extensions.yml) | ![pending](https://img.shields.io/badge/-pending-lightgrey) |
| [`haybarn-python`](https://github.com/Query-farm-haybarn/haybarn-python) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-python?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-python/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-python/haybarn-python.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-python/actions/workflows/haybarn-python.yml) | ![pending](https://img.shields.io/badge/-pending-lightgrey) |
| [`haybarn-iceberg`](https://github.com/Query-farm-haybarn/haybarn-iceberg) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-iceberg?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-iceberg/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-iceberg/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-iceberg/actions/workflows/MainDistributionPipeline.yml) | ![pending](https://img.shields.io/badge/-pending-lightgrey) |
| [`haybarn-ducklake`](https://github.com/Query-farm-haybarn/haybarn-ducklake) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-ducklake?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-ducklake/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-ducklake/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-ducklake/actions/workflows/MainDistributionPipeline.yml) | ![pending](https://img.shields.io/badge/-pending-lightgrey) |

> Badges are live — click through for the latest run. A grey "pending" cell means we haven't started the rebase onto that base version yet.

## Design principles

- **Hard fork, small patch stack.** One commit, one concern — easy to rebase onto each new DuckDB release.
- **Rename the artifacts, not the API.** `haybarn` CLI, `libhaybarn.*`, but the `duckdb::` C++ namespace, headers, and CMake package name are unchanged. ABI-compatible by design.
- **Sign everything.** Binaries via GPG + cosign. Extensions verified against a single Haybarn RSA key — DuckDB-signed extensions won't load.
- **Build-fork extensions, don't rebrand them.** `INSTALL iceberg` still installs `iceberg`. The Haybarn-ness is *built-against-Haybarn + signed-by-Haybarn*, not a new name.

## Getting started

Pick your barn door:

- 🦆 **CLI** — grab a release from [`haybarn` releases](https://github.com/Query-farm-haybarn/haybarn/releases).
- 🐍 **Python** — `pip install haybarn` (coming soon to PyPI), then `import haybarn as duckdb`.
- 🧊 **Extensions** — install in-engine; they fetch from `haybarn-extensions.query.farm`.

## Trademark & independence

Haybarn is an independent project. It is **not endorsed by, affiliated with, or sponsored by the DuckDB Foundation**. We build on the upstream MIT-licensed DuckDB source and document our modifications in each repo's `NOTICE` and patch stack.

> **DuckDB is a trademark of the DuckDB Foundation.**

For DuckDB trademark questions, the Foundation can be reached at `quack@duckdb.org`. For Haybarn, write to us at `hello@query.farm`.

## License

Haybarn inherits DuckDB's MIT license. See each repo's `LICENSE` and `NOTICE`.

---

<div align="center">
<sub>Built with care by <a href="https://query.farm">Query Farm LLC</a> · <code>hello@query.farm</code></sub>
</div>
