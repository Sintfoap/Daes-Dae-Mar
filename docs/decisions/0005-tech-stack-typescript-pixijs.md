# 0005. Tech stack direction: TypeScript + PixiJS

Date: 2026-08-18
Status: Accepted

## Context

`docs/game-design/01-open-questions.md` Q7 needed a resolved direction
before Phase 2 prototyping. `docs/technical-design/01-tech-stack-options.md`
laid out two genuinely viable candidates — Godot (C#) and a web stack
(TypeScript + PixiJS) — noting both satisfy the architecture in
`00-architecture-overview.md` equally well, and framed it as a
workflow/distribution preference rather than a capability gap.

## Decision

Target stack: **TypeScript, with PixiJS for 2D rendering.**

## Consequences

- Content files can be plain JSON with no engine-specific import step,
  which lines up cleanly with `docs/technical-design/02-data-driven-content.md`'s
  emphasis on human-readable, diffable content files.
- Distribution defaults to a browser link — zero install for playtesters,
  which matters given the project plans on external playtesting (Phase 6
  in `ROADMAP.md`).
- TypeScript's static typing supports the determinism and schema
  validation goals in `00-architecture-overview.md` and
  `02-data-driven-content.md` well.
- Grid/tilemap tooling, hex-grid support in particular
  (`0003-hex-grid.md`), will need more hand-building than Godot would have
  provided out of the box — flagged as real Phase 2 prototyping work, not
  a blocker.
- Desktop packaging (if wanted later) is deferred — straightforward via
  something like Tauri or Electron if it becomes a priority, per
  `01-tech-stack-options.md`, but not needed for the browser-first plan.
- `docs/technical-design/01-tech-stack-options.md` should be updated to
  record this as decided rather than open, and Phase 2's tactical-battle
  prototype (`ROADMAP.md`) should be built directly in this stack.
