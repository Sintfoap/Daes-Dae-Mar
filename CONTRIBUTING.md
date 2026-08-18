# Contributing

Right now (Phase 1) this project is entirely documentation — see
`ROADMAP.md` for the phase plan. The most valuable contribution at this
stage is working through `docs/game-design/01-open-questions.md`.

## Current workflow

1. Read `README.md`, then `docs/game-design/00-pillars-and-pitch.md` for
   context.
2. Check `docs/game-design/01-open-questions.md` for what's still
   undecided.
3. Propose changes to design/technical docs as normal edits — this is
   early enough that docs should be edited directly and iterated on, not
   treated as fixed specs.
4. If a change resolves an open question or overrides a documented
   default for a non-obvious reason, add an ADR in `docs/decisions/` (see
   that folder's `README.md`) and link it from the resolved question.
5. Update `ROADMAP.md` checkboxes as work completes.

## Once code exists (Phase 2+)

See `docs/technical-design/05-contributing-guide.md` for the target
workflow for adding units, factions, and other content, plus code
conventions once a tech stack is chosen.

## Documentation conventions

- Every doc under `docs/` starts with a `> Status: Draft / Stable /
  Superseded` line so readers know how settled it is.
- Cross-reference other docs by relative path rather than duplicating
  their content.
- Keep the glossary (`docs/game-design/02-glossary-wot-to-game-terms.md`)
  current — it's the map from Wheel of Time vocabulary to actual game
  systems, and every doc leans on it.
