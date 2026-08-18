# Campaign & Progression

> Status: Draft — depends on Q5/Q6 in `01-open-questions.md`.

## Campaign structure options

- **A — Sandbox conquest (CoE5-style).** No scripted plot; factions
  compete over the bounded map until a win condition (last faction
  standing, control-X-provinces, or a turn limit with a scoring model) is
  met. Highly replayable, matches CoE5's own structure closely.
- **B — Scripted timeline campaign.** A fixed narrative arc (e.g., Shadow
  strength escalating toward a Last Battle endgame) with scripted events
  regardless of player faction. More thematic payoff, less replayable,
  much higher writing/content cost.
- **C — Hybrid.** Sandbox play (A) with an optional escalating
  Shadow-strength/Last-Battle countdown running in the background as a
  soft campaign clock and occasional scripted event, without fully
  scripting the outcome.

**Recommendation: C.** It keeps replayability (core to a CoE5-style game
with this much faction variety) while giving the setting's signature
throughline — the Shadow rising, building toward Tarmon Gai'don — real
mechanical presence instead of leaving the campaign feeling directionless.
The exact shape of the "clock" is a follow-up design question once Phase 3
validates the base sandbox loop.

## Victory conditions (draft, pending A/B/C decision above)

- Territorial control threshold within the bounded map
- Faction-specific alternate win conditions (e.g., White Tower "restore
  order," Shadow "corrupt/conquer past a threshold," matching each
  faction's strategic hook from `05-factions.md`) — flagged as a strong
  option for making victory itself feel asymmetric, not just the path
  there
- A turn-limit scoring fallback if no faction reaches a hard win condition

## Heroes and persistence

- Commanders/heroes (per `07-units.md`) persist across the campaign and
  can be permanently lost (death, capture, stilling/gentling for
  channelers) — this is what gives channeling's risk real teeth at the
  campaign level, not just within one battle.
- Recommend heroes gain experience/veterancy over a campaign (a light
  leveling system) so a surviving hero is worth protecting beyond their
  base stats — exact leveling depth is a Phase 5 content question.

## The Horn of Valere (illustrative campaign-level relic/event)

A possible example of a campaign-defining event system: a rare, discoverable
artifact that, once found and used, calls forth legendary hero units for
whichever faction controls it — extremely high strategic value, and
therefore something factions might contest specifically, giving the
campaign a natural mid-to-late-game flashpoint. Flagged as an illustrative
design pattern (rare relic → major swing event) worth reusing for other
WoT artifacts, not a commitment to build the Horn specifically at MVP.

## Replayability levers

Matching CoE5's own replay hooks:
- Random or player-selected faction each campaign
- Random event tables (raids, Foretellings, defections, Forsaken
  awakenings)
- Faction/map combinations changing the strategic texture even on a
  fixed map

## Open items

- Full turn-limit/scoring model — depends on A/B/C decision above
- Hero leveling depth — Phase 5
- Whether losing your capital/last province is an immediate game-over or
  a faction can be reduced to a rump state and continue — recommend
  immediate elimination for MVP simplicity, revisit if playtesting wants
  comeback mechanics
