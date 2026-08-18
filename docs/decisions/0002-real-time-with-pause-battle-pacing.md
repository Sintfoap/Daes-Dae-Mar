# 0002. Real-time-with-pause battle pacing

Date: 2026-08-18
Status: Accepted

## Context

`docs/game-design/04-tactical-battle-layer.md` needed a resolved model for
how the player gives orders during a tactical battle
(`docs/game-design/01-open-questions.md` Q1). The drafted recommendation
was turn-based/simultaneous resolution, on the reasoning that it best fits
a grid, avoids real-time engineering complexity, and reads more like a
deliberate "thinking person's battle." The alternative, real-time with
pause, is the model the Total War half of this project's pitch is
explicitly drawing from.

## Decision

Battles run on a continuous clock. The player can pause at any time to
survey the field and queue orders without time pressure, then unpause to
watch them execute. Movement, combat, and channeling all happen in real
time (while paused, nothing advances) rather than resolving in discrete
simultaneous rounds.

## Consequences

- The battle layer keeps its "no reflex pressure required" property
  (pillar 3, non-goals in `docs/game-design/00-pillars-and-pitch.md`) via
  unlimited pausing, not via turn structure — the design docs' language
  needed updating to reflect that the guarantee comes from the pause
  mechanic, not from a lack of a clock.
- The simulation needs a fixed-timestep, deterministic tick loop under the
  hood (à la lockstep RTS simulation) to keep the determinism requirement
  in `docs/technical-design/00-architecture-overview.md` intact — orders
  are timestamped to simulation ticks, not wall-clock time. This is a
  heavier technical lift than turn-based/simultaneous resolution would
  have been, but is well-precedented (this is how most real-time strategy
  games achieve deterministic replay/lockstep).
- Weave "cast steps" (`docs/game-design/06-magic-and-channeling.md`) become
  visible cast-time windows on the clock (interruptible while casting)
  rather than a discrete phase within a round — mechanically similar
  intent, different implementation.
- Morale/combat resolution shifts from "resolved once per round" to
  "ongoing, continuous" — attack cooldowns instead of per-round exchanges.
  `docs/technical-design/04-battle-simulation-design.md` was rewritten to
  match.
- This is a genuinely higher-risk system to prototype than the
  turn-based alternative would have been — Phase 2's tactical prototype
  should treat "does the fixed-tick real-time-with-pause loop actually
  feel good on a hex grid" as its top validation question.
