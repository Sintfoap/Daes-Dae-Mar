# Project Structure

> Status: Draft — describes the intended repo layout once code starts in
> Phase 2/3. No source directories exist yet; this doc is the plan they'll
> follow when they're created, so the structure is decided deliberately
> rather than accreting ad hoc.

## Proposed top-level layout

```
/
├── docs/
│   ├── game-design/         # what the game is (see docs/game-design/)
│   ├── technical-design/    # how it's built (this folder)
│   └── decisions/           # ADRs — see decisions/README.md
├── content/                 # data-driven content files (Phase 3+)
│   ├── factions/
│   ├── units/
│   ├── weaves/
│   ├── terrain/
│   ├── items/
│   └── events/
├── src/                     # simulation, presentation, AI code (Phase 2+)
│   ├── strategic/
│   ├── tactical/
│   ├── content/             # loading/validation of the content/ folder
│   ├── ai/
│   └── presentation/
├── assets/                  # portraits, icons, audio, UI art
├── tools/                   # content validation scripts, dev tooling
├── tests/
├── ROADMAP.md
├── CONTRIBUTING.md
└── README.md
```

## Rationale

- **`content/` is separate from `src/`** deliberately, even though most
  engines would let you colocate them — this makes the "content vs. code"
  boundary from `02-data-driven-content.md` visible at the filesystem
  level, not just as a convention someone has to remember. A contributor
  adding a unit should never need to open `src/`.
- **`src/` mirrors the architecture doc's boundaries** (`strategic/`,
  `tactical/`, `ai/`, `presentation/`, plus `content/` for the
  loader/validator code that reads the top-level `content/` folder) —
  matching `00-architecture-overview.md`'s system boundaries 1:1 so the
  code structure and the architecture doc never drift apart.
- **`tools/`** holds the content-validation tooling called out in
  `02-data-driven-content.md`, plus anything else that supports authoring
  (e.g., a script that scaffolds a new unit file from a template).
- **`docs/decisions/`** holds ADRs — see that folder's own README for the
  convention. Keeping decisions in the repo, next to the code/docs they
  affect, is part of "robust and easy to add to": a future contributor (or
  future us) can find out *why* something is the way it is without asking.

## Naming conventions (to establish once code starts)

- Content file IDs (the `id` field in `02-data-driven-content.md`'s
  example) should be `lowercase_snake_case` and globally unique across
  their content type.
- Source files should follow whatever the chosen engine/language's
  idiomatic convention is (this intentionally isn't fixed yet, pending
  `01-tech-stack-options.md`).

## Open items

- This structure is a plan, not yet reality — it should be created
  incrementally as Phase 2/3 actually needs each folder, not scaffolded
  wholesale as empty directories today. Revisit and adjust once real code
  exists and the plan meets reality.
