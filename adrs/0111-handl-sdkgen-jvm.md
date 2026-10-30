---
title: Handl SDK Generator — JVM Backend
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed.
---


# ADR-0111: Handl SDK Generator — JVM Backend

## Decision


Add a `plugin-sdkgen-backend-jvm` crate that parses Java class / method
signatures (directly or from `.class` / `.jar` metadata) and produces
`SdkgenModule` records.

- The backend may start by consuming a list of Java method signatures or a
  reflection dump; later it can read `.class` files or use a lightweight parser.
- The `client_package` for the generated adapter is `jvm`.
- The adapter uses `jvm.call` / `jvm.exception` primitives (a new `jvm` client
  package similar to `ffi`) to invoke methods and translate exceptions into
  `Result<_, JvmException>`.
- Map common Java types to Handl types:
  - `int` / `Integer` → `Int` (`i32`)
  - `long` / `Long` → `Int` (`i64`)
  - `double` / `Double` → `Float` (`f64`)
  - `String` → `String` (`jstring`)
  - `byte[]` / `ByteBuffer` → `Bytes` (`jbyte_array`)
  - Object references → `Handle` (`jobject`)
  - `void` → `()`
- Support class-name to package mapping, method overloads via name mangling, and
  static vs instance method dispatch.


## Why

[ADR-0107 — Handl SDK Generator](./0107-handl-sdk-generator.md) established a backend-agnostic IR (`SdkgenModule`) and a port-adapter emitter architecture. The first concrete backend is C / libclang. The next high-priority backend is the JVM, which lets Handl call Java libraries and native Java classes through JNI.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- Handl can consume the huge ecosystem of JVM libraries.
- A `jvm` client package must be designed and implemented, paralleling `ffi`.
- Overloaded Java methods require a name-mangling scheme in the port.
- This backend is higher priority than Bukkit / Spigot / Paper (ADR-0112) and

## Enforcement

- `plugin-sdkgen-backend-jvm` — where this is true.

## Design

The full record (context, tables, phases, trade-offs): [`design/0111-handl-sdkgen-jvm.md`](../design/0111-handl-sdkgen-jvm.md).
