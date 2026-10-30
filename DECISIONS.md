---
title: Decisions
type: index
---

# Decisions

One line per decision rule, generated from each ADR's `## Decision`
section with `host/scripts/gen-decisions.py`. The ADR is the argument;
this is the recall surface (ADR-0161 §8). Superseded records are excluded.

### Handl SDK Generator — Windows and macOS C Backend Support

- Add target-aware include / sysroot lookup: — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- Linux: -I/usr/include and the libclang resource directory — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- macOS: the macOS SDK path (xcrun --show-sdk-path or SDKROOT) and — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- Windows: the MSVC / Clang system include set and Windows-style paths — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- Map the target triple to the correct shared-object name at emitter time: — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- libc.so.6 for Linux glibc — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- libSystem.dylib for macOS — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- *.dll for Windows — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- Allow the user to pass an explicit target triple — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)
- Preserve the existing port / adapter split and the SdkgenModule IR; only — [ADR-0110](adrs/0110-handl-sdkgen-windows-macos.md)

### Handl SDK Generator — JVM Backend

- The backend may start by consuming a list of Java method signatures or a — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- The client_package for the generated adapter is jvm — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- The adapter uses jvm.call / jvm.exception primitives (a new jvm client — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- Map common Java types to Handl types: — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- int / Integer → Int (i32) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- long / Long → Int (i64) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- double / Double → Float (f64) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- String → String (jstring) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- byte[] / ByteBuffer → Bytes (jbyte_array) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- Object references → Handle (jobject) — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- void → () — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)
- Support class-name to package mapping, method overloads via name mangling, and — [ADR-0111](adrs/0111-handl-sdkgen-jvm.md)

### Handl SDK Generator — Bukkit, Spigot, Paper Backend

- The Bukkit backend accepts a manifest of Bukkit / Spigot / Paper class — [ADR-0112](adrs/0112-handl-sdkgen-bukkit-spigot-paper.md)
- It reuses the JVM IR and the jvm client package — [ADR-0112](adrs/0112-handl-sdkgen-bukkit-spigot-paper.md)
- It adds event-hook generation so Bukkit events can be exposed as Handl graded — [ADR-0112](adrs/0112-handl-sdkgen-bukkit-spigot-paper.md)
- A .sdkgen.yaml file selects the target platform (bukkit / spigot / — [ADR-0112](adrs/0112-handl-sdkgen-bukkit-spigot-paper.md)
- The first target is Spigot / Paper on Linux x86_64 because that is the most — [ADR-0112](adrs/0112-handl-sdkgen-bukkit-spigot-paper.md)
