# Strategic Layer

> Status: Draft — depends on Q4/Q5/Q6 in `01-open-questions.md`.

## Model: CoE5, not Civ

The strategic layer is a **shared turn**, not a round-robin. Every faction
on the map — player and AI alike — plans and resolves its turn's actions
together, the way Conquest of Elysium's cults and nations do. There is no
"the player acts, then we cut to the AI acting one at a time." This matters
for tone as much as mechanics: the player should feel like one actor among
several actors pursuing their own agendas, not the sole protagonist with
scenery that reacts to them.

## The map

- Divided into **provinces** (discrete territories, not free-form
  coordinates) — matches CoE5's territory model and keeps the strategic
  layer legible at a glance.
- Provinces have a **terrain type** (plains, hills, forest, river,
  fortified town, Blight-corrupted, etc.) that feeds both economy
  (resource yield) and the tactical layer (a battle fought in a forest
  province starts with forest terrain on the battle grid — see
  `04-tactical-battle-layer.md`).
- Scope is a **bounded region** at MVP, not the whole continent (see Q6).

## Turn structure

Each strategic turn, a faction (player or AI) may, subject to its own
faction-specific toolkit:

1. **Move commanders/armies** between adjacent (or fast-traveled)
   provinces.
2. **Recruit units** in provinces it controls, limited by that province's
   resources and the faction's recruitment rules.
3. **Spend strategic-scale magic** where applicable (Foretelling for
   intel, Traveling/gateways for movement, Compulsion-adjacent effects for
   subversion, scrying for reconnaissance) — see `06-magic-and-channeling.md`.
4. **Build/upgrade** province infrastructure (garrisons, resource
   improvements, Waygate access, fortifications).
5. **React to events** — random or triggered occurrences (raids, defections,
   Foretellings, Forsaken awakenings) that create decisions, not just
   flavor text.

When two hostile armies end a turn in the same province, a **tactical
battle** triggers — see `04-tactical-battle-layer.md`.

## Faction agency (the CoE5 signature feature)

Every faction's toolkit should differ enough that no two factions play the
strategic layer the same way. This is the property that makes CoE5 replay
well, and it should be a hard design requirement here, not an aspiration:

- The **White Tower** recruits by influence and Ajah politics, not just
  gold; it can pull strings across the map without moving an army.
- The **Seanchan** expand by conquest-and-collar — capturing enemy
  channelers converts them into damane, so Seanchan strategic play is
  explicitly predatory toward channeling factions.
- The **Shadow** plays an infiltration/corruption game in addition to open
  war — provinces can turn without a battle ever being fought.
- The **Aiel** don't hold territory the way settled nations do; their
  strategic incentives are different (raiding, honor, clan politics) from
  a nation trying to hold a border.

If a faction's strategic-layer decisions could be reskinned onto another
faction with just a name change, that faction isn't done yet.

## Fog of war and information

Recommend real fog of war (you know what your scouts/channelers/spies can
see), with channeling-based scrying as a way to buy information at a
resource cost — this gives Foretelling/sensing weaves real strategic value,
not just tactical value.

## Diplomacy

CoE5 has minimal-to-no diplomacy between AI factions; conflict is mostly
emergent from competing for the same territory/resources. Recommend
following that lead for MVP — simple non-aggression/alliance flags at most,
not a full negotiation system — and revisiting depth here only if
playtesting in Phase 3 shows the lack of it hurts. This keeps a
notoriously scope-hungry system out of the MVP critical path.

## Open items

- Exact number of provinces in the MVP region and their terrain
  distribution — belongs in a follow-up map-design pass once Q6 is
  resolved.
- Whether commanders/heroes are a scarce, individually-tracked resource
  (CoE5-style) — recommended yes, ties into `09-campaign-and-progression.md`.
