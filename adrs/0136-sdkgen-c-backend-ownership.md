---
title: '`sdkgen-c` backend ownership'
type: adr
date: 2026-10-28
status: accepted
status_note: Accepted — extracted in ADR-0128 Phase 2 (`modules/sdkgen-c`).
---

# ADR-0136: `sdkgen-c` backend ownership

## Context

[ADR-0107](../0107-handl-sdk-generator.md) defines the SDK generator as a
port: `SdkgenBackend` → `SdkgenModule` → `Emitter`, with a *target record*
`(backend_id, emitter_id)`. Today the dispatcher in `plugin-ext-sdkgen`
hard-codes `if kind != "c" && …` plus a `match` arm per target.

## Decision

`c` owns the **C backend**: `plugin-sdkgen-backend-c` — the C ABI model, the
header/`clang-sys` layer, and the C-specific emitter primitives — plus the
platform C-binding ADRs ([ADR-0110](../0110-handl-sdkgen-windows-macos.md),
[ADR-0111](../0111-handl-sdkgen-jvm.md),
[ADR-0112](../0112-handl-sdkgen-bukkit-spigot-paper.md)) and the `-c` package
block with its `generated/*-c-linux-x86_64/` outputs.

`host` keeps the port (`SdkgenTarget` descriptor + registry) and the
cross-cutting `plugin-sdkgen` IR / `plugin-sdkgen-emitter-file`.

## Consequences

- `clang-sys` leaves the platform lock and build.
- `python` depends on this module at *target* level: `hnl sdkgen python` is
  backend `c` + emitter `python`, so the registry key is the target record,
  not a crate.
- Adding a C-family target is an edit here plus a registry entry in the
  consuming host — never a change to the platform dispatcher.
