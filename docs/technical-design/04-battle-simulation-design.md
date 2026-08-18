# Battle Simulation — Technical Design

> Status: Draft — technical counterpart to
> `docs/game-design/04-tactical-battle-layer.md`. Assumes that doc's
> recommended answers (turn-based/simultaneous resolution, square grid,
> one-token-per-unit) unless noted. This is the doc Phase 2's tactical
> prototype should be validating.

## Grid representation

A square grid, sized per `docs/game-design/01-open-questions.md` Q3
(roughly 9–13 × 14–20). Each cell holds:
- Terrain type (references a `terrain` content item —
  `02-data-driven-content.md`)
- Occupancy (at most one unit token per cell, or a small stack if design
  later allows it — recommend starting with strictly one for simplicity)
- Line-of-sight/elevation data derived from terrain (e.g., hills block
  sight to cells behind them)

## Turn/round structure

Matches `docs/game-design/04-tactical-battle-layer.md`'s battle-phase
model:

1. **Order phase** — both sides (player input + AI decision-making)
   produce a full set of orders for the round with no time pressure. No
   simulation state changes during this phase; it's pure planning against
   a frozen snapshot of the board.
2. **Resolution phase** — orders from both sides are applied together,
   deterministically, following a fixed resolution order (cast steps →
   movement → attacks → morale, per the game design doc). This phase has
   no player input; it plays out from the two order sets.
3. Repeat, checking end conditions (rout, destruction, round limit) after
   each resolution phase.

This maps cleanly onto a **command-pattern** style implementation: an
order is a data object (unit ID, order type, target cell/unit), the
resolution phase is a pure function of `(board state, order set) → (new
board state, resolution log)`. That purity is what makes determinism
(`00-architecture-overview.md`) straightforward here rather than aspirational
— there's no hidden mutable state or timing dependency for it to leak
through.

## Strategic ↔ tactical interchange

When the strategic layer triggers a battle, it needs to hand the tactical
simulation:
- The two (or more) forces involved (unit IDs + current state — a
  channeler's current taint/Power reserve carries over from the strategic
  layer, since it's a campaign-persistent value per
  `docs/game-design/06-magic-and-channeling.md`)
- The province's terrain, translated into a grid layout
- Any battle-specific modifiers (e.g., a siege's fortification state)

And the tactical simulation needs to hand back:
- Surviving units and their post-battle state (including any taint/
  burnout/injury changes)
- Casualties/losses
- The battle outcome (decisive win/loss, mutual retreat, etc.) for the
  strategic layer to act on

This contract should be defined as its own data shape early in Phase 2 —
it's the seam between the two biggest systems in the game, and getting it
wrong is expensive to fix later. Recommend prototyping it literally first,
before either simulation's internals are fully built, precisely so this
seam gets validated early rather than discovered late.

## Combat resolution (placeholder)

Actual formulas are a balance concern deferred to a later pass (flagged in
`docs/game-design/04-tactical-battle-layer.md`'s open items), but
structurally, resolution for one engagement should be a pure function of:
`(attacker stats + tags, defender stats + tags, terrain modifiers, facing/
flank state) → (damage, morale impact)` — no hidden randomness beyond an
explicit, seeded RNG call whose seed is part of the deterministic replay
state.

## AI within the battle

The tactical AI (per `00-architecture-overview.md`) produces a full order
set during the order phase using the same order data structures the player
uses — there's no special-cased "AI order" type. This keeps the AI honest
(it can't do anything the player couldn't also do) and keeps the
resolution phase agnostic to who issued which orders.

## What Phase 2's prototype specifically needs to answer

- Does the order-phase/resolution-phase split actually feel like "active
  micro" to a player, or does it feel closer to a puzzle/chess turn? (Both
  are viable, but which one this lands as should inform UI pacing and
  whether e.g. an "undo last order" affordance is needed during the order
  phase.)
- Is the resolution order (cast → move → attack → morale) legible when
  watched, or does it need an intermediate visualization step per
  sub-phase?
- Does the strategic↔tactical data contract hold up once both sides are
  prototyped against it, or does it need fields neither side anticipated?

## Open items

- Final combat formulas — balance pass, Phase 6.
- Whether resolution phases play out with animation the player watches, or
  resolve instantly with a log the player can review — a presentation
  question, but one worth deciding early since it affects pacing
  expectations; no recommendation yet, flagged for Phase 2 prototype
  feedback.
