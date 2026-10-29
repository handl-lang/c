---
title: Task 0128 — `c/` extraction (ADR-0128 Phase 2)
type: task
date: 2026-10-28
---

# Task 0128 — `c/` extraction (ADR-0128 Phase 2)

Expand ADR-0128 Phase 2 for this repo. The docs are already on
this `project` branch; the code lands with the extraction.

## Docs owned here

- `adrs/0136-sdkgen-c-backend-ownership.md` — sdkgen-c backend ownership
- split parent `0107-handl-sdk-generator.md` (canonical half stays in `platform`)

## Extraction

- [ ] Follow ADR-0128 Phase 2: create the repo's workspace,
      move the crates/packages named there, wire the git dep + `[patch]`.
- [ ] Keep `main` a clean build tree (`/project/` ignored).
- [ ] Flip the split children from `Proposed` to `Accepted` when the
      code actually moves.
