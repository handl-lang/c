# c

The **C target** — C ABI bindings, the libclang-backed C backend, and the
C-family SDK emitters (ADR-0136; the generator port itself is ADR-0107).

## What this repo owns

| what | where |
|---|---|
| `plugin-sdkgen-backend-c` — the C ABI model, the header/`clang-sys` layer, and the C emitter primitives | `modules/sdkgen-c` (ADR-0128 Phase 2) |
| the C-family platform bindings — Windows/macOS, JVM, Bukkit/Spigot/Paper | ADRs 0110–0112 |
| the `-c` package block and its `generated/*-c-<triple>/` outputs | `packages/` |

`host` keeps the port (`SdkgenTarget` descriptor + registry) and the
cross-cutting `plugin-sdkgen` IR. Adding a C-family target is an edit here plus
a registry entry in the consuming host — never a change to the platform
dispatcher. `clang-sys` therefore leaves the platform lock and build.

## Status

Initialized from the org `project` tree. The module extraction (ADR-0128
Phase 2) has not started: the backend still builds from
[`sdkgen-c`](https://github.com/handl-lang/sdkgen-c), and the JVM / Bukkit
targets from `sdkgen-*` repos.

## Development

No build here yet — nothing is extracted. When `modules/sdkgen-c` lands it
follows the engine-* shape: `ci.sh` as the gate (fmt → clippy → test → doc) and
a committed `bupha.toml`.

## Documentation

Published site (Diátaxis): <https://handl-lang.github.io/docs/c/>

Decision records live on the `project` branch under `project/adrs/`; the
layout rule is ADR-0162 (`host` repo, `project` branch).

## License

MIT.
