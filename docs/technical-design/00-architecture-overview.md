# Architecture Overview

> Status: Draft — describes the intended shape of the system. No code
> exists yet (Phase 1/2); this doc guides Phase 2 prototyping and Phase 3
> production architecture, and will be revised once real code exists to
> check it against.

## Guiding technical principle

The user's explicit ask is a game that's **robust and easy to add to from
a human perspective.** For this project, that translates to one concrete
architectural priority above all others: **content (factions, units,
weaves, terrain, items, events) must live in data, not in code.** A
contributor adding a new Aiel unit should be authoring a data file and an
icon, not touching the battle simulation. See
`02-data-driven-content.md` for the specifics.

Everything else in this doc is in service of that.

## System boundaries

```
┌─────────────────────────────────────────────────────────┐
│                      Content / Data Layer                 │
│  Factions, units, weaves, terrain types, items, events —  │
│  defined in data files, validated against schemas.        │
└───────────────┬─────────────────────────┬─────────────────┘
                 │                         │
       ┌─────────▼─────────┐     ┌─────────▼─────────┐
       │  Strategic Layer    │     │  Tactical Battle   │
       │  Simulation          │◄───┤  Simulation         │
       │  (turns, provinces,  │    │  (grid, terrain,    │
       │   resources, AI)     │    │   orders, combat)   │
       └─────────┬────────────┘    └─────────┬───────────┘
                 │                            │
                 └──────────────┬─────────────┘
                                 │
                       ┌─────────▼─────────┐
                       │   Presentation      │
                       │  (rendering, UI,    │
                       │   input)            │
                       └─────────────────────┘
```

- **Content/Data Layer** — the source of truth for "what exists in the
  game." Owns nothing about *how* simulations run, only *what* they run
  on. See `02-data-driven-content.md`.
- **Strategic Layer Simulation** — owns the map, provinces, turn
  resolution, faction AI at the strategic level, and resource accounting.
  Hands off to the tactical layer when a battle triggers, and receives the
  battle's outcome back (see `04-battle-simulation-design.md` for the
  interchange contract).
- **Tactical Battle Simulation** — owns the grid, terrain instancing,
  order queue, and combat/morale resolution for a single battle. Doesn't
  know anything about the strategic map beyond what it was handed to set
  up the battle.
- **Presentation** — rendering, UI, input handling. Deliberately kept as
  thin a layer as possible over the simulations, so simulation logic stays
  testable without a renderer (important for a turn-based, order-queue
  design where "was this the right outcome given these orders" needs to be
  verifiable independent of animation).

## Why this split matters for "easy to add to"

- A contributor adding **content** never touches the two simulation
  systems.
- A contributor changing **battle rules** (e.g., tuning morale) never
  touches the strategic layer.
- A contributor changing **strategic rules** (e.g., how provinces yield
  resources) never touches battle resolution.
- The **presentation layer** can be reworked (art style changes, UI
  changes) without risk to simulation correctness, because it's a
  consumer of simulation state, not an owner of it.

This is a fairly standard simulation/presentation split, chosen
specifically because the project's stated risk (a novel tactical battle
mechanic, a large content roster) benefits most from strict boundaries
around content and around the battle simulation specifically.

## Determinism

Both simulations should be **deterministic given their inputs** (same
starting state + same orders/RNG seed → same outcome). This isn't just
good practice — the tactical battle layer's whole pitch
(`docs/game-design/04-tactical-battle-layer.md`) depends on the player
being able to reason about what an order will do. A non-deterministic
combat resolution undermines the "thinking person's battle" pillar
directly. It also keeps the door open for replays or future multiplayer
without an architecture rewrite, even though neither is in scope now.

## AI

Two distinct AI problems, not one:
- **Strategic AI** — faction-level decision making (what to recruit,
  where to move, whether to attack) — needs to produce faction *identity*
  (per `docs/game-design/05-factions.md`), not just competent play.
- **Tactical AI** — battle-level order-giving for the AI side of a battle
  — needs to be competent enough that AI-vs-AI battles (which happen
  constantly in a CoE5-style shared world, off-screen from the player) and
  player-vs-AI battles both feel like real opposition.

These should be architected as separate systems consuming the same
content data, not one shared "AI brain" — their decision timescales and
inputs are too different to share cleanly.

## What Phase 2 needs to validate about this

- That the strategic/tactical hand-off contract (what a "battle setup"
  looks like as data passed from one system to the other) is actually
  clean in practice, not just on paper.
- That determinism is achievable at the performance/complexity level the
  turn-based battle model actually needs (should be low-risk given the
  turn-based, non-real-time decision in
  `docs/game-design/01-open-questions.md` Q1, but worth confirming).

## Open items

- Final engine/tech stack — see `01-tech-stack-options.md`; this overview
  is intentionally engine-agnostic so it survives that decision.
- Save/load format — deferred until content schemas
  (`02-data-driven-content.md`) stabilize, since save format is largely a
  function of what state needs persisting.
