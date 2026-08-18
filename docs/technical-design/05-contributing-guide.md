# Contributing Guide (Technical)

> Status: Draft — the workflow steps below describe intent for once code
> and content pipelines exist (Phase 4+). Kept here now so the target
> workflow is designed deliberately, the same way the rest of the
> architecture is. See root `CONTRIBUTING.md` for the short version and
> current (Phase 1) reality.

## Adding a new unit (target workflow, once `content/units/` exists)

1. Copy the nearest existing unit file in `content/units/<faction>/` as a
   starting template, or use a scaffolding script in `tools/` if one
   exists by then.
2. Fill in the stat block per the template in
   `docs/game-design/07-units.md` and the schema in
   `docs/technical-design/02-data-driven-content.md`.
3. Add a portrait/icon asset under `assets/portraits/`.
4. Run the content validator (`tools/`) to confirm the file is
   well-formed and all referenced IDs resolve.
5. Playtest the unit in at least one battle before committing — a unit
   that validates but has never been fielded is unfinished.
6. If the unit introduces a new tag/mechanic not covered by
   `docs/game-design/07-units.md`, update that doc in the same change —
   design docs and content should never drift apart.

No simulation code should need to change for this workflow. If it does,
that's a signal the archetype/tag system in `07-units.md` and
`02-data-driven-content.md` is missing something general-purpose — fix the
general system, not just this one unit.

## Adding a new faction

Follow the checklist at the bottom of `docs/game-design/05-factions.md`
first — a faction needs its four-question design brief answered before
any content files get written. Then:

1. Add the faction definition file under `content/factions/`.
2. Add its initial unit roster under `content/units/<faction>/`, per the
   unit workflow above.
3. Add any faction-unique weaves/items it needs.
4. Update `docs/game-design/05-factions.md` from "brief" to "designed"
   status.

## Adding a new weave, terrain type, or item

Same pattern: data file under the relevant `content/` subfolder, validated,
cross-referenced from the design doc it belongs to
(`docs/game-design/06-magic-and-channeling.md` for weaves/items,
`docs/game-design/04-tactical-battle-layer.md` for terrain).

## Recording decisions

Any decision that isn't obvious from the code/data itself — especially
ones that override or narrow a documented default — should get a short
ADR in `docs/decisions/` (see that folder's README for the template). Rule
of thumb: if a future contributor might reasonably ask "wait, why does it
work this way instead of the more obvious way?", write it down.

## Documentation standards

- Every new system gets a doc in `docs/game-design/` and/or
  `docs/technical-design/` before or alongside its implementation, not
  after — Phase 1's whole premise is designing before building, and that
  discipline should hold for new systems added later too.
- Docs use the `> Status: Draft / Stable / Superseded` convention at the
  top (see any existing doc for the pattern) so a reader always knows how
  much to trust a given page.
- Cross-reference liberally (as this whole doc set already does) —
  duplicated explanations drift out of sync; links don't.

## Code conventions

Deferred until the tech stack (`01-tech-stack-options.md`, Q7) is decided
— will be filled in once there's a real language/engine to write
conventions for. Placeholder principles that will apply regardless of
stack:
- The content/code boundary (`02-data-driven-content.md`) is not
  optional — code review should reject hardcoded content.
- Simulation code stays deterministic and free of direct rendering/UI
  calls (`00-architecture-overview.md`).

## Commit / PR conventions

Standard practice: small, focused commits with descriptive messages;
one logical change per PR; update the relevant doc(s) in the same PR as
the change they describe, not in a follow-up. Full detail deferred until
there's a real contributor workflow (more than one person/session working
concurrently) to write conventions against.
