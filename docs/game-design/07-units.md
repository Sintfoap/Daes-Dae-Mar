# Units

> Status: Draft — framework only. Full rosters populate per-faction as
> each faction enters the build queue (see `05-factions.md` checklist).

## Unit archetypes

Every unit in the game, regardless of faction, is built from one of these
archetypes. Archetypes exist so the tactical battle layer's rules
(`04-tactical-battle-layer.md`) only need to reason about a handful of
behavioral categories, even as the faction roster grows large.

| Archetype | Battlefield role | Example |
|---|---|---|
| Line infantry | Holds ground, anchors formations | Whitecloak men-at-arms |
| Skirmisher / ranged | Damage at range, weak in melee | Aiel bowmen, Seanchan archers |
| Shock cavalry | Fast, strong charge bonus, weak sustained melee | Borderlander lancers |
| Channeler | High-impact weaves, fragile, resource-limited (see `06-magic-and-channeling.md`) | Aes Sedai, Asha'man, Dreadlord, damane |
| Hero / commander | Unique named unit, morale anchor, often has a special ability | A named Aiel clan chief, a Forsaken |
| Beast / shadowspawn | Non-human, often faction-exclusive rules | Trolloc, raken, grolm |
| Siege | Slow, specialized against fortifications | Trebuchet-equivalent, breaching tools |

A given faction typically fields 4–7 archetypes with faction-specific
flavor, not all 7 — the Aiel notably field no shock cavalry at all, which
is itself a piece of faction identity (see `05-factions.md`).

## Stat template

Every unit's stat block should cover, at minimum:

- **Strength/HP** — how much punishment the unit (as an abstracted
  squad/company, not an individual) can take
- **Attack** — melee and/or ranged offense
- **Defense** — mitigation, separate from HP
- **Move** — grid cells per order
- **Morale** — baseline resistance to routing (see
  `04-tactical-battle-layer.md`)
- **Special tags** — flags like *cannot be flanked from forest*, *ambush
  bonus*, *fear aura*, *channeler (see weave list)*, *no cavalry counter*,
  etc. — this is where most of a unit's actual personality lives, more
  than in the raw numbers

## Representation and scale

Per Q3 in `01-open-questions.md`: one grid token represents an abstracted
squad/company of soldiers (CoE5-style single-icon-per-unit), not an
individual combatant. Strength/HP represents the unit's remaining fighting
power as a whole, not hit points on one body.

## Example unit cards (illustrative, not final)

**Whitecloak Man-at-Arms** (Children of the Light, Line infantry)
- Solid stats across the board, formation bonus when adjacent to another
  Whitecloak infantry unit, no special vulnerability to Compulsion/fear
  effects (unwavering faith) but no channeling counter-tools baseline —
  those come from separate specialist units.

**Aiel Spear (Warrior Society)** (Aiel, Line infantry / skirmisher hybrid)
- Below-average Defense but above-average Attack and Move; large bonus in
  forest/hill terrain; morale penalty when fighting in open ground away
  from cover — mechanically pushes the player toward choosing terrain
  deliberately, per pillar 3.

**Asha'man Soldier** (Black Tower, Channeler)
- Small Power reserve relative to full Aes Sedai, but can also fight
  competently in melee (unlike most channeler units) — reflects the
  Black Tower's martial-first training; gains taint per weave cast, with a
  visible taint-meter tracked across the campaign, not just the battle.

**Damane (handled)** (Seanchan, Channeler — unique pairing rule)
- Strong ranged-weave offense but must remain within a short range of its
  paired sul'dam handler unit or suffers major penalties/becomes
  uncontrollable — makes protecting (or targeting) the handler a real
  tactical thread distinct from any other channeler unit in the game.

## Heroes and named units

Ta'veren, Wolfbrothers, Forsaken, clan chiefs, and similar named
individuals are Hero/Commander archetype units with:
- A unique ability not available to generic units of their type
- A morale-anchor effect on nearby friendly units
- Campaign-persistence — heroes can be lost permanently (death, capture,
  stilling/gentling) with real strategic consequences, which is what makes
  them worth protecting rather than just strong stat sticks

Full hero design (leveling, acquisition, loss consequences) belongs in
`09-campaign-and-progression.md`.

## Open items

- Full per-faction rosters — populated as each faction is greenlit (see
  `05-factions.md` build-queue checklist)
- Exact numeric balancing — a Phase 6 concern, not a Phase 1 blocker
- Whether unit *upgrades* exist (a unit gaining equipment/veterancy over a
  campaign) or units are strictly recruited-at-fixed-stats — recommend
  deferring this to `09-campaign-and-progression.md` since it's really a
  campaign-structure question more than a unit-design one
