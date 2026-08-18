# Battle Simulation — Technical Design

> Status: Draft — technical counterpart to
> `docs/game-design/04-tactical-battle-layer.md`. Reflects the locked
> decisions in `docs/decisions/0002-real-time-with-pause-battle-pacing.md`
> (real-time with pause), `docs/decisions/0003-hex-grid.md` (hex grid), and
> `docs/decisions/0006-strategic-driven-entry-and-deployment.md`
> (entry edge set by the strategic attack direction, asymmetric deployment
> zones). This is the doc Phase 2's tactical prototype should be
> validating most directly — it's the riskiest technical piece in the
> project.

## Grid representation

A hex grid, sized per `docs/game-design/01-open-questions.md` Q3 (roughly
9–13 × 14–20, still open). Recommend **axial coordinates** (two integers
per hex) for simulation code — simplest to store and diff, convertible to
cube coordinates when a calculation (distance, line-of-sight, ring/range
queries) is easier to express that way. Each hex holds:
- Terrain type (references a `terrain` content item —
  `02-data-driven-content.md`)
- Occupancy (at most one unit token per hex, or a small stack if design
  later allows it — recommend starting with strictly one for simplicity)
- Line-of-sight/elevation data derived from terrain (e.g., hills block
  sight to hexes behind them)

Adjacency is 6-directional. Pathfinding is hex-grid A* (a well-documented
problem — the classic reference is Amit Patel's Red Blob Games hex-grid
guide) rather than anything novel; budget real implementation time for it
in Phase 2, but not design-risk time.

## Orientation: canonical simulation space vs. rendered space

Per `docs/decisions/0006-strategic-driven-entry-and-deployment.md`, the
edge an attacker enters from varies battle to battle based on the
strategic map. Recommend keeping the **simulation itself orientation-
agnostic**: internally, combat/movement/order logic always treats "the
attacker's entry edge" as a canonical direction (equivalent to one fixed
axial direction, e.g. what the code calls "north" regardless of what the
strategic map calls it), so resolution logic, pathfinding, and flanking
math never need to special-case which real-world direction a battle is
facing.

The **presentation layer** is what maps canonical simulation space onto
the direction the player actually attacked from — rotating the rendered
hex grid (and camera, and UI anchoring) so that, e.g., an attack launched
from a province to the west visually enters from the west of the screen.
This keeps a whole class of orientation bugs out of simulation code
entirely and localizes the "which way is this battle actually facing"
concern to a single, thin rotation/mapping step at render time. The
strategic-layer province-direction data
(`docs/game-design/03-strategic-layer.md`) is the input to that mapping,
computed once when a battle is set up.

## Deployment zone geometry

Per `docs/decisions/0006-strategic-driven-entry-and-deployment.md`, the
two sides' deployment zones are asymmetric and both are subsets of the hex
grid, computed from the canonical entry edge above:

- **Attacker zone:** hexes within a fixed ring-distance of the entry edge
  (a "beachhead" band). Simple to compute as a hex-distance-from-edge
  query once the entry edge is known.
- **Defender zone:** all hexes *not* in the attacker zone and not in a
  small neutral buffer immediately in front of it — i.e., most of the
  board. This should be expressed as a straightforward exclusion, not a
  separately-authored shape, so it stays correct automatically regardless
  of which edge the attacker is entering from or how the map's terrain is
  laid out.

Exact ring-distance/buffer sizes are a Phase 2 tuning question (tracked in
`docs/game-design/04-tactical-battle-layer.md`'s open items), but the
computation should be a pure function of `(entry edge, board shape) →
(attacker zone, defender zone)` for the same reason the orientation
mapping above is kept out of simulation logic — it needs to work
correctly for any entry edge without bespoke cases.

## Simulation clock

Per `docs/decisions/0002-real-time-with-pause-battle-pacing.md`, the
battle plays out in real time from the player's perspective, but the
underlying simulation runs on a **fixed timestep** ("tick"), the same
pattern deterministic real-time/RTS games use for lockstep simulation and
replay support:

- The simulation advances in discrete ticks (e.g., 10–20 ticks per
  simulated second — exact rate is a Phase 2 tuning question) regardless
  of rendering frame rate.
- **Pause** simply stops ticks from advancing; nothing in the simulation
  changes while paused. This is what makes "pause and think forever" free
  — there's no real-time cost to pausing, only simulated-time cost, and
  simulated time isn't advancing.
- **Orders** issued by the player (or produced by the AI) are queued
  against a specific future tick, not executed instantly against
  wall-clock time — this is what keeps the simulation deterministic (same
  tick + same order queue → same outcome) despite presenting as free-
  flowing real time.
- Movement along a hex path, attack cooldowns, and weave cast-time windows
  are all expressed as tick counts internally (e.g., "this unit's attack
  has a cooldown of N ticks," "this weave has a cast window of M ticks
  before it resolves and can be interrupted by damage or by the caster
  being forced to move").

This tick-based approach is what makes the real-time-with-pause decision
compatible with the project's determinism requirement
(`00-architecture-overview.md`) — it's a heavier lift than the originally-
drafted turn-based/simultaneous model would have been, but it's
well-precedented territory, not a novel risk.

## Strategic ↔ tactical interchange

When the strategic layer triggers a battle, it needs to hand the tactical
simulation:
- The two (or more) forces involved (unit IDs + current state — a
  channeler's current taint/Power reserve carries over from the strategic
  layer, since it's a campaign-persistent value per
  `docs/game-design/06-magic-and-channeling.md`)
- The province's terrain, translated into a hex layout
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
structurally, an engagement between two adjacent units resolves
continuously via **attack cooldowns**: each unit has an attack rate (ticks
between attacks), and while in range and not disrupted, damage/morale
impact apply on each attack tick as a pure function of
`(attacker stats + tags, defender stats + tags, terrain modifiers, facing/
flank state) → (damage, morale impact)` — no hidden randomness beyond an
explicit, seeded RNG call whose seed is part of the deterministic
simulation state (seeded per-battle, advanced deterministically per tick,
not per wall-clock event).

## AI within the battle

The tactical AI (per `00-architecture-overview.md`) issues orders
continuously using the same order data structures and the same tick-queue
mechanism the player uses — there's no special-cased "AI order" type and
no privileged information. This keeps the AI honest (it can't do anything
the player couldn't also do) and keeps the simulation agnostic to who
issued which orders.

## Rendering vs. simulation

Because the simulation runs on fixed ticks and rendering runs on frame
rate, the presentation layer should **interpolate** unit positions/
animations between the last two simulated ticks for smooth visual movement
across a hex, rather than snapping units hex-to-hex. This is the specific
technical answer to the earlier design-doc concern about "grid combat in
real time looking janky" — the simulation stays discrete and deterministic
underneath, while the player only ever sees smooth motion.

## What Phase 2's prototype specifically needs to answer

- Does the tick rate feel responsive when unpaused, and does pausing
  genuinely feel free of time pressure? This is the core bet behind
  `docs/decisions/0002-real-time-with-pause-battle-pacing.md` and needs
  real validation, not just a paper argument.
- Does hex-grid movement/pathfinding read clearly to a player watching it
  play out in real time (as opposed to reviewing it turn-by-turn, which is
  more forgiving of ambiguity)?
- Does the strategic↔tactical data contract hold up once both sides are
  prototyped against it, or does it need fields neither side anticipated?
- Is a visible weave cast-time window (per
  `docs/game-design/04-tactical-battle-layer.md`) actually legible and
  interruptible in practice, or does it need a more explicit UI treatment
  than "a bar over the unit's head"?
- Does the canonical-simulation/rotated-rendering split above actually
  hold up cleanly, or does some piece of gameplay logic (line-of-sight,
  UI anchoring, camera behavior) turn out to need real-world orientation
  awareness after all?

## Open items

- Exact tick rate — Phase 2 tuning.
- Final combat formulas — balance pass, Phase 6.
- Whether the interpolation/rendering approach above needs client-side
  prediction of any kind, or whether ticks are always computed before
  being rendered (recommend the latter for MVP simplicity — no networked
  multiplayer is in scope, so there's no latency to hide).
