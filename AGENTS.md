# c

The **C target** — C ABI bindings, the libclang-backed C backend, and
the C-family SDK emitters (ADR-0136; the generator port itself is
ADR-0107).

## Layout (planned — ADR-0128 Phase 2)

| what | where |
|---|---|
| `plugin-sdkgen-backend-c` — the C ABI model, header/`clang-sys` layer, C emitter primitives | `modules/sdkgen-c` |
| C-family platform bindings — Windows/macOS, JVM, Bukkit/Spigot/Paper | ADRs 0110–0112 |
| the `-c` package block and `generated/*-c-<triple>/` outputs | `packages/` |

## Contract

- `host` keeps the port (`SdkgenTarget` descriptor + registry) and the
  cross-cutting `plugin-sdkgen` IR. Adding a C-family target is an edit
  here plus a registry entry in the consuming host — never a change to
  the platform dispatcher.
- Status: initialized from the org `project` tree; module extraction
  has not started — the backend still builds from
  [`sdkgen-c`](https://github.com/handl-lang/sdkgen-c).

## Verification

No build yet — nothing is extracted. When `modules/*` lands it follows
the engine-* shape: `workflows/gate.yaml` as the gate (fmt → clippy → test → doc) and
a committed `bupha.toml`.

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
