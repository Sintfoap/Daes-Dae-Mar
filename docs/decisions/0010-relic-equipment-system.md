# 0010. Cross-faction relic equipment system: channeler-gated vs. universal

Date: 2026-08-18
Status: Accepted

## Context

Relics (angreal/sa'angreal/ter'angreal) already existed as a resource
(`docs/game-design/08-economy-and-resources.md`) and as channeler
equipment (`docs/game-design/06-magic-and-channeling.md`), but only as
"equipment for channelers" in general — there was no rule for whether a
non-channeling faction could ever use one, and no faction-level flavor on
who's good at finding or using them. The user asked to generalize relics
into a real collectible-equipment system attachable to commanders/heroes
broadly, and to work out which factions can best find or use them —
raised alongside the White Tower discussion because the Oath Rod (ADR
0009) is the first concrete instance of a named, singular relic.

## Decision

Relics split into two equipment tiers by access rule, not just by canon
category:

- **Angreal / Sa'angreal — channeler-gated.** Only a Channeler-archetype
  unit can socket one. This restricts them to channeling factions: White
  Tower, Black Tower, Shadow (Dreadlords/Black Ajah), Seanchan (damane).
  A non-channeling faction that finds one can't use it personally —
  trade it, hold it as diplomatic leverage, or (Whitecloaks specifically)
  destroy it on principle.
- **Ter'angreal — universal by default.** Any Hero/Commander-archetype
  unit can use one regardless of channeling ability, unless that specific
  item's own definition says otherwise. This is what gives non-channeling
  factions a real reason to care about the relic economy. Canon-grounded
  example: the foxhead medallion (blocks the One Power from affecting its
  wearer) needs no channeling ability and is a natural Whitecloak item.

Faction-level relic flavor (first pass, to be refined once specific items
are authored):
- **White Tower:** best at safely *identifying* unknown relics (Brown
  Ajah scholarship); holds the Oath Rod by default (`0009`).
- **Black Tower:** more willing to experiment — faster attunement,
  higher backlash risk on failure.
- **Shadow:** access to a unique tier of Age-of-Legends/corrupted relics
  no other faction can find, usually at a taint/corruption cost to use.
- **Seanchan:** the a'dam collar *is* their signature ter'angreal
  (already their whole damane mechanic); a general bonus to finding/
  cataloguing relics (Seekers).
- **Aiel:** their territory is unusually relic-rich (Rhuidean, Age of
  Legends remnants) — a bonus to *finding* relics on Aiel land, even
  though Aiel custom keeps most Aiel from personally using them, which is
  a deliberate trade/diplomacy hook with other factions.
- **Whitecloaks:** may destroy found angreal/sa'angreal rather than trade
  them (doctrine), but happily use a channeling-blocking ter'angreal like
  the foxhead medallion without contradiction.
- **Borderlands/Andor:** no special relic rule — the unmarked baseline
  case.

## Consequences

- `docs/game-design/06-magic-and-channeling.md`'s Relics section and
  `docs/game-design/08-economy-and-resources.md`'s Relics resource row
  both needed rewriting to state the channeler-gated/universal split
  explicitly, rather than "equipment for channelers" generally.
- `docs/game-design/07-units.md`'s Heroes and named units section gained
  a relic-slot rule for Hero/Commander units generally (not just
  channelers), since ter'angreal are now usable by any of them.
- This is the second named, singular relic pattern in the docs (after the
  Oath Rod) — worth watching whether "a few unique, world-defining
  relics plus many generic/interchangeable ones" becomes a real design
  pattern worth naming, or whether it stays ad hoc per relic.
- Real open items: exact identification/attunement mechanics (a skill
  check? a risk table?); how many singular named relics should exist
  total (too many and they stop feeling special; too few and most
  factions never interact with the system); whether Aiel's
  relic-rich-but-culturally-restrained position gets its own dedicated
  mechanic or stays flavor until Aiel's own deep-dive.
