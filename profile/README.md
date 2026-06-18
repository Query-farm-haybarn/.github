<div align="center">

<img src="./assets/haybarn-icon.png" alt="Haybarn" width="160" />

# Haybarn

**An independent derived distribution of DuckDB.**
*Powered by DuckDB. Published by [Query Farm LLC](https://query.farm).*

<img src="./assets/haybarn-banner.png" alt="A red barn full of hay bales, set against rolling green hills" width="100%" />

</div>

---

> [!IMPORTANT]
> **Haybarn 1.5.4 is in release-candidate phase.** Current tag is
> `haybarn-v1.5.4-rc1`, built from **upstream DuckDB v1.5.4**. The engine,
> on-disk format, and APIs are inherited from upstream and will not change
> between rcs — only Haybarn's packaging, signing, and extension catalog are
> still settling. Install snippets below pin the `rc` channel explicitly; once
> `1.5.4` final ships, the `@rc` / `==…` suffixes go away. (`1.5.3` already
> shipped final.)

## What is Haybarn?

Haybarn is a friendly, independent rebuild of [DuckDB](https://duckdb.org) — branded, signed, and shipped on its own cadence by **Query Farm LLC**. Think of it as the local barn down the road from the duck pond: same grain, different roof.

We rebuild DuckDB from source into our own signed binaries and pair them with a self-contained, signed extension ecosystem. Haybarn stays **ABI-compatible** with upstream DuckDB so forward-porting is cheap and your existing code keeps working.

> *"Haybarn, powered by DuckDB."*

## Why a barn?

Because barns are where you keep what the fields produce — sturdy, dependable, full of useful things stacked neatly out of the rain. That's how we want our distribution to feel.

## What's in here

**Engine & CLI**

| Repo | What it is |
| --- | --- |
| [`haybarn`](https://github.com/Query-farm-haybarn/haybarn) | Core fork of DuckDB. The `haybarn` CLI and `libhaybarn`. |

**Language bindings**

| Repo | What it is |
| --- | --- |
| [`haybarn-python`](https://github.com/Query-farm-haybarn/haybarn-python) | Python bindings — `import haybarn` (or `import haybarn as duckdb`). |
| [`haybarn-rust`](https://github.com/Query-farm-haybarn/haybarn-rust) | Rust crates — `haybarn`, `libhaybarn-sys`, `haybarn-loadable-macros` (fork of `duckdb-rs`), on crates.io. |
| [`haybarn-node-neo`](https://github.com/Query-farm-haybarn/haybarn-node-neo) | Node bindings — `@haybarn/node-api` (fork of `duckdb-node-neo`), on npm. |
| [`haybarn-jdbc`](https://github.com/Query-farm-haybarn/haybarn-jdbc) | JDBC driver — `farm.query.haybarn:haybarn_jdbc` (fork of `duckdb-java`), on Maven Central. |
| [`haybarn-wasm`](https://github.com/Query-farm-haybarn/haybarn-wasm) | Haybarn compiled to WebAssembly (`@haybarn/haybarn-wasm`, React + shell packages). |
| [`haybarn-ios`](https://github.com/Query-farm-haybarn/haybarn-ios) | Native iOS app — run SQL on local data, with a built-in Claude data agent. |

**Extension build-forks** (rebuilt against the Haybarn engine, Haybarn-signed)

| Repo | What it is |
| --- | --- |
| [`haybarn-iceberg`](https://github.com/Query-farm-haybarn/haybarn-iceberg) | Apache Iceberg extension. |
| [`haybarn-ducklake`](https://github.com/Query-farm-haybarn/haybarn-ducklake) | DuckLake extension. |
| [`haybarn-delta`](https://github.com/Query-farm-haybarn/haybarn-delta) | Delta Lake extension. |
| [`haybarn-httpfs`](https://github.com/Query-farm-haybarn/haybarn-httpfs) | HTTP(S) + S3 filesystem extension. |
| [`haybarn-community-extensions`](https://github.com/Query-farm-haybarn/haybarn-community-extensions) | The full community catalog (250+ extensions), rebuilt and Haybarn-signed. |

> Plus internal CI/infra repos (`haybarn-extension-ci-tools`, `haybarn-community-extensions-sync`, `haybarn-status`, …) that build, sign, and track everything above.

Extensions install just like upstream:

```sql
INSTALL iceberg;  LOAD iceberg;     -- a core build-fork
INSTALL h3 FROM community;          -- anything from the community catalog
```

The core set Haybarn builds and signs includes `httpfs`, `delta`, `iceberg`,
`ducklake`, `spatial`, `aws`, `azure`, `avro`, the `postgres`/`mysql`/`sqlite`
scanners, `vss`, `fts`, `excel`, and more — alongside the 250+ community
extensions. Everything is served from `haybarn-extensions.query.farm/{core,community}`
and signed with the Haybarn extension key.

## Build status

Each row is a Haybarn repo; the CI column tracks its current build against
**DuckDB v1.5.4**. Badges are live — click through for the latest run.

| Repo | Latest release | CI (DuckDB **v1.5.4**) |
| --- | :---: | :---: |
| [`haybarn`](https://github.com/Query-farm-haybarn/haybarn) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn/releases) | [![release CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn/haybarn-release.yml?branch=haybarn&label=release)](https://github.com/Query-farm-haybarn/haybarn/actions/workflows/haybarn-release.yml) <br> [![extensions CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn/haybarn-extensions.yml?branch=haybarn&label=extensions)](https://github.com/Query-farm-haybarn/haybarn/actions/workflows/haybarn-extensions.yml) |
| [`haybarn-python`](https://github.com/Query-farm-haybarn/haybarn-python) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-python?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-python/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-python/haybarn-python.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-python/actions/workflows/haybarn-python.yml) |
| [`haybarn-rust`](https://github.com/Query-farm-haybarn/haybarn-rust) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-rust?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-rust/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-rust/haybarn-rust.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-rust/actions/workflows/haybarn-rust.yml) |
| [`haybarn-node-neo`](https://github.com/Query-farm-haybarn/haybarn-node-neo) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-node-neo?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-node-neo/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-node-neo/haybarn-node-neo.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-node-neo/actions/workflows/haybarn-node-neo.yml) |
| [`haybarn-jdbc`](https://github.com/Query-farm-haybarn/haybarn-jdbc) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-jdbc?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-jdbc/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-jdbc/haybarn-jdbc.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-jdbc/actions/workflows/haybarn-jdbc.yml) |
| [`haybarn-wasm`](https://github.com/Query-farm-haybarn/haybarn-wasm) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-wasm?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-wasm/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-wasm/main.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-wasm/actions/workflows/main.yml) |
| [`haybarn-iceberg`](https://github.com/Query-farm-haybarn/haybarn-iceberg) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-iceberg?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-iceberg/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-iceberg/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-iceberg/actions/workflows/MainDistributionPipeline.yml) |
| [`haybarn-ducklake`](https://github.com/Query-farm-haybarn/haybarn-ducklake) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-ducklake?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-ducklake/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-ducklake/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-ducklake/actions/workflows/MainDistributionPipeline.yml) |
| [`haybarn-delta`](https://github.com/Query-farm-haybarn/haybarn-delta) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-delta?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-delta/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-delta/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-delta/actions/workflows/MainDistributionPipeline.yml) |
| [`haybarn-httpfs`](https://github.com/Query-farm-haybarn/haybarn-httpfs) | [![release](https://img.shields.io/github/v/release/Query-farm-haybarn/haybarn-httpfs?include_prereleases&display_name=tag&label=)](https://github.com/Query-farm-haybarn/haybarn-httpfs/releases) | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-httpfs/MainDistributionPipeline.yml?branch=haybarn&label=build)](https://github.com/Query-farm-haybarn/haybarn-httpfs/actions/workflows/MainDistributionPipeline.yml) |
| [`haybarn-community-extensions`](https://github.com/Query-farm-haybarn/haybarn-community-extensions) | — | [![CI](https://img.shields.io/github/actions/workflow/status/Query-farm-haybarn/haybarn-community-extensions/build_all.yml?branch=main&label=catalog)](https://github.com/Query-farm-haybarn/haybarn-community-extensions/actions/workflows/build_all.yml) |

> For a single live dashboard that aggregates **all** Haybarn build, release,
> and extension-catalog runs in one place, see
> **<https://haybarn-status.query.farm>**.

## Design principles

- **Hard fork, small patch stack.** One commit, one concern — easy to rebase onto each new DuckDB release.
- **Rename the artifacts, not the API.** `haybarn` CLI, `libhaybarn.*`, but the `duckdb::` C++ namespace, headers, and CMake package name are unchanged. ABI-compatible by design.
- **Sign everything.** Release artifacts carry detached GPG signatures + SLSA build-provenance attestations. Extensions are verified against a single Haybarn RSA key — DuckDB-signed extensions won't load.
- **Build-fork extensions, don't rebrand them.** `INSTALL iceberg` still installs `iceberg`. The Haybarn-ness is *built-against-Haybarn + signed-by-Haybarn*, not a new name.

## Getting started

Pick your barn door:

- 🦆 **CLI** — three ways, same binary:
  ```sh
  npx haybarn@rc                    # via npm
  uvx haybarn-cli==1.5.4rc1         # via PyPI — live (or `pipx run …`)
  # or grab the zip from https://github.com/Query-farm-haybarn/haybarn/releases
  ```
- 🐍 **Python** — `import haybarn as duckdb`. (The `haybarn-cli` package is live
  on PyPI; the `haybarn` *library* wheel publish is wired up and building green
  per push, with the first PyPI release still in progress.)
- 🦀 **Rust** — `cargo add haybarn -F bundled` (fork of `duckdb-rs`; also
  publishes `libhaybarn-sys` and `haybarn-loadable-macros` to crates.io).
- 🟢 **Node** — `npm install @haybarn/node-api`; drop-in for `@duckdb/node-api`
  (just swap the import source).
- ☕ **JDBC** — on Maven Central as `farm.query.haybarn:haybarn_jdbc`; JDBC URLs
  are `jdbc:haybarn:…` and the driver is `farm.query.haybarn.HaybarnDriver`.
  ```xml
  <dependency>
    <groupId>farm.query.haybarn</groupId>
    <artifactId>haybarn_jdbc</artifactId>
    <version>1.5.4</version>
  </dependency>
  ```
- 🌐 **WASM** — `@haybarn/haybarn-wasm` for the browser; 📱 **iOS** — native app in [`haybarn-ios`](https://github.com/Query-farm-haybarn/haybarn-ios).
- 🧊 **Extensions** — install in-engine just like upstream: `INSTALL iceberg; LOAD iceberg;`.
  Core lives at `https://haybarn-extensions.query.farm/core`, community at
  `/community` — both signed with the same Haybarn key.

Checking what's currently green:

- 🚦 **Status dashboard** — <https://haybarn-status.query.farm> aggregates
  every Haybarn workflow across every repo in one view.

Every release artifact ships with a **SLSA build-provenance attestation**:

```sh
gh attestation verify haybarn_cli-linux-amd64.zip \
  --repo Query-farm-haybarn/haybarn
```

## Switching from DuckDB

Haybarn is a *drop-in* derived distribution. If your code uses DuckDB today,
this section is the cheat sheet for moving to Haybarn.

### What stays the same

- **Your existing `.duckdb` database files just work.** Haybarn uses the same
  on-disk format as upstream v1.5.4.
- **The C/C++ API.** `duckdb::` namespace, public headers (`duckdb.h` /
  `duckdb.hpp`), the `DUCKDB_VERSION` macro, and the `.duckdb_extension`
  suffix are all preserved. Haybarn is ABI-compatible.
- **SQL.** Same dialect, same functions, same planner — it is the DuckDB engine.
- **Extension names.** `INSTALL iceberg`, `INSTALL spatial`, etc. work
  unchanged — we don't rebrand extensions, we rebuild and sign them.

### What changes

| Area | DuckDB | Haybarn |
|---|---|---|
| CLI binary | `duckdb` | `haybarn` |
| Shared library | `libduckdb.{so,dylib,dll}` | `libhaybarn.{so,dylib,dll}` |
| Python import | `import duckdb` | `import haybarn` (or `import haybarn as duckdb`) |
| Python package | `duckdb` | `haybarn` (`haybarn-cli` for the packaged CLI) |
| Node package | `@duckdb/node-api` | `@haybarn/node-api` |
| Rust crate | `duckdb` | `haybarn` (`libhaybarn-sys`, `haybarn-loadable-macros`) |
| JDBC artifact / URL | `org.duckdb:duckdb_jdbc` · `jdbc:duckdb:` | `farm.query.haybarn:haybarn_jdbc` · `jdbc:haybarn:` |
| Extension cache dir | `~/.duckdb/extensions/` | `~/.haybarn/extensions/` |
| Extension trust root | DuckDB Foundation key | A single Haybarn RSA key |
| Extension repository | `extensions.duckdb.org` | `haybarn-extensions.query.farm/{core,community}` |
| Release signing | — | GPG detached signatures + SLSA build provenance |

The big behavioural one: **DuckDB-signed extensions will not load in Haybarn,
and Haybarn-signed extensions will not load in DuckDB.** They're cryptographically
disjoint ecosystems by design. If an extension you depend on isn't yet in the
Haybarn catalog, open an issue on `Query-farm-haybarn/haybarn-community-extensions`.

### Step-by-step migration

1. **Install the Haybarn CLI** alongside (or in place of) `duckdb`:
   ```sh
   npx haybarn@rc   # or `uvx haybarn-cli==1.5.4rc1`
   ```
2. **Open your existing database** with `haybarn yourdb.duckdb` — no migration,
   no schema rewrite. The file format is identical.
3. **Re-install your extensions** so the local cache gets the Haybarn-signed
   builds (`INSTALL iceberg; INSTALL spatial; …`). Old cached blobs under
   `~/.duckdb/extensions/` are ignored by Haybarn; you can leave them or
   delete them.
4. **For Python projects**, change one import:
   ```python
   import haybarn as duckdb   # rest of your code is unchanged
   ```
   For third-party code you can't edit, an opt-in shim:
   ```python
   import haybarn.compat   # registers `haybarn` as the `duckdb` module
   import duckdb           # now resolves to Haybarn
   ```
5. **CI / Dockerfiles** — replace `duckdb` invocations with `haybarn`, swap
   `pip install duckdb` for `pip install haybarn` (when the wheel publish goes
   live; until then, install from `Query-farm-haybarn/haybarn-python`).

### When *not* to switch (yet)

- You need an extension that hasn't been rebuilt for Haybarn. The core set and
  250+ community extensions are already live, but the catalog isn't 100% of
  upstream yet — check `Query-farm-haybarn/haybarn-community-extensions` and
  open an issue if something you need is missing.
- You depend on OS-level code signing (Apple notarization, Windows
  Authenticode). Haybarn ships GPG + SLSA attestations today; OS code signing
  is on the roadmap, not in the box.
- You're on the DuckDB nightly channel. Haybarn tracks tagged releases only.

### Going back

Going back to upstream DuckDB is symmetric — the `.duckdb` file works there
too. The only friction is re-installing extensions against the DuckDB trust
root.

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
