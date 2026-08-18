# Tech Stack Options

> Status: Draft — needs your decision (Q7 in
> `docs/game-design/01-open-questions.md`). This doc lays out the
> tradeoffs; Phase 2 prototyping should validate the choice with real code
> before Phase 3 commits to it for good.

## What the game actually needs from an engine

Given the design so far:
- 2D only — no 3D rendering requirement at all (pillar 1: icon/portrait
  presentation)
- Grid-based simulation with a turn-based, non-real-time battle model —
  no hard real-time performance pressure
- Two nested turn-based simulations (strategic + tactical) with a
  data-driven content pipeline as the top technical priority
- A UI-heavy interface (province management, unit orders, faction info
  panels) — likely as much UI work as simulation work
- A solo or very small team building it, prioritizing approachability and
  iteration speed over raw performance

This profile favors **engines/stacks strong at 2D and UI, not 3D or raw
performance**, and favors **data-file-first workflows** (the engine should
make "define a unit in a data file" natural, not fight it).

## Candidate A — Godot (GDScript or C#)

- Free, open-source, purpose-built for 2D, strong tilemap/grid tooling
  out of the box, solid UI/theming system.
- GDScript is approachable to write and read; C# is available if
  stronger typing/tooling is preferred.
- Native support for resource files (`.tres`) that fit a data-driven
  content approach well, plus straightforward JSON import if a
  human-editable/diff-friendly format is preferred for content files (see
  `02-data-driven-content.md`).
- Ships as a real desktop app on Windows/Mac/Linux with minimal packaging
  friction.
- Large, active strategy/tactics-game community precedent to draw on.

**Best fit if:** the priority is a real desktop application, approachable
scripting, and the strongest out-of-the-box 2D/tilemap tooling.

## Candidate B — Web stack (TypeScript + a 2D renderer like PixiJS, UI in
plain HTML/CSS or a framework)

- Runs in a browser — zero-install distribution, trivial to share a build
  with a playtester via a link.
- TypeScript gives strong typing for the simulation layers, which pairs
  well with a determinism requirement and with schema-validated content
  data (JSON content files are a completely natural fit — no import step
  needed at all).
- UI-heavy screens (province panels, faction info, unit cards) are
  arguably *easier* to build well in HTML/CSS than in a game engine's UI
  system.
- Packaging as a desktop app later (via something like Tauri or Electron)
  is straightforward if that's wanted eventually.
- Weaker out-of-the-box tilemap/grid tooling than Godot — more of that
  gets hand-built, though for a simple square grid (per Q2) this is not a
  large lift.

**Best fit if:** the priority is easy distribution/sharing, a
TypeScript-first codebase, and treating content files as plain JSON with
no engine-specific import step.

## Candidate C — Unity (C#)

- Included for completeness. Strong general-purpose engine, huge
  ecosystem, but its strengths (3D, physics, asset store) are mostly
  unused by this design's requirements, and its licensing/footprint is
  heavier than Godot's for a project that is deliberately 2D and simple.

**Not recommended** — Godot covers the same 2D/C# territory this project
actually needs, with a lighter footprint and no licensing overhead to
track.

## Recommendation

Between A and B specifically (both are genuinely good fits — this is a
real decision, not a formality):

- If you'd rather work in a real game engine, with the strongest built-in
  2D/grid tooling and a native desktop app as the default output: **Godot
  (C#)**. C# over GDScript specifically because the simulation layers
  (deterministic, data-schema-driven) benefit from static typing.
- If you'd rather work in a web-native stack, want zero-install
  shareability by default, and want content files to be plain JSON with
  no engine import step: **TypeScript + PixiJS**.

Both satisfy the architecture in `00-architecture-overview.md` equally
well — this is a workflow/distribution preference, not a capability
gap. Worth deciding based on which stack you'd rather spend time reading
and writing, since that's the more durable factor over the life of the
project.

## Open items

- Final decision (Q7) — yours to make; Phase 2 should prototype the
  tactical battle grid in the chosen stack specifically to confirm it
  before Phase 3 commits.
- Once decided, this doc should be updated to record the choice and
  rationale, and a corresponding ADR added to `docs/decisions/`.
