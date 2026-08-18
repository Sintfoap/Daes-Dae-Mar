# Data-Driven Content

> Status: Draft — this is the technical doc most directly answering the
> user's "robust and easy to add to" requirement. Treat changes here as
> high-impact.

## Philosophy

Every faction, unit, weave, terrain type, and item described in
`docs/game-design/` should exist in the running game as **data**, loaded
and validated at startup, not as hardcoded classes or branching logic.
The simulation code should be able to say "run this unit's stat block
through combat resolution" without knowing or caring whether that unit is
a Whitecloak man-at-arms or an Aiel spear — the difference lives entirely
in the data.

This is the single most important technical decision for the project's
stated goal of being easy to add to from a human perspective: adding
faction #6 should look like adding files, not writing code.

## What lives in data

| Content type | Defines |
|---|---|
| **Faction** | Identity, strategic-layer recruitment rules, resource priorities, playable unit list, faction-specific flags (e.g., "no channelers," "no cavalry") |
| **Unit** | Archetype, stat block, special tags, weave list (if a channeler), portrait/icon reference |
| **Weave** | Category, cost, effect, cast-step behavior, which factions/tiers can use it |
| **Terrain type** | Movement cost, combat modifiers, line-of-sight rules |
| **Item (relic)** | Effect, acquisition rules, which unit types can equip it |
| **Event** | Trigger conditions, effects, narrative text |

Each of these corresponds directly to a concept already defined in the
game design docs (see the cross-references in
`docs/game-design/02-glossary-wot-to-game-terms.md`) — the data schema
should be a fairly direct translation of those docs, not a reinterpretation
of them. If a schema field doesn't map back to something in the design
docs, that's worth a second look in either direction.

## Format

Recommend plain, human-readable, diffable data files — JSON or YAML,
final choice can follow from the tech stack decision in
`01-tech-stack-options.md` (e.g., Godot's native `.tres` format is also an
option if that stack is chosen, but plain JSON kept alongside it is worth
considering purely for human editability and version-control diffs, which
matter a lot for "easy to add to").

Whatever the format, every content file should be:
- **Validated against a schema** at load time (or at a CI check), so a
  malformed unit file fails loudly and immediately, not as a mysterious
  runtime bug three systems away.
- **One file per content item** where practical (one file per unit, one
  per faction), not one giant file per content type — this keeps diffs
  small and ownership clear when multiple people/sessions are adding
  content.

## Example shape (illustrative, not a final schema)

```json
{
  "id": "aiel_spear",
  "faction": "aiel",
  "archetype": "line_infantry",
  "display_name": "Aiel Spear",
  "stats": { "strength": 12, "attack": 7, "defense": 4, "move": 4, "morale": 8 },
  "tags": ["terrain_bonus:forest", "terrain_bonus:hill", "morale_penalty:open_ground", "no_cavalry_counter"],
  "portrait": "portraits/aiel_spear.png"
}
```

This is deliberately close to the stat template in
`docs/game-design/07-units.md` — the data schema should never drift far
from the design doc's own vocabulary, or the two will silently disagree
over time.

## Content validation as a first-class workflow step

Recommend a schema-validation check (ideally automated — a script run in
CI or pre-commit once code exists) that every content file must pass:
required fields present, referenced IDs (e.g., a unit's faction ID, a
weave's referenced effect) actually resolve, no duplicate IDs. This is
cheap to build early and expensive to retrofit once dozens of content
files exist — worth building alongside the *first* content files in Phase
3/4, not deferring to Phase 5 when the roster is large.

## What stays in code

- The simulation engines themselves (turn resolution, combat resolution,
  order processing) — the *rules* the data is interpreted by.
- AI decision-making logic (though AI *tuning parameters* — how
  aggressively a faction recruits, e.g. — are a good candidate for data
  too, once the AI architecture exists).
- Rendering/UI.

The line: **if it's "what exists," it's data. If it's "how the game
processes what exists," it's code.**

## Open items

- Final file format (JSON vs YAML vs engine-native) — depends on Q7.
- Schema definition language/tooling (e.g., JSON Schema, or a
  code-generated schema from the eventual engine's type system) — a Phase
  2/3 decision once the stack is chosen.
- Versioning strategy for content files as schemas evolve (so old saves or
  old content don't silently break) — flagged for `03-project-structure.md`
  and revisited once saves exist.
