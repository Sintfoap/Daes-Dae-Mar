# 0007. Headcount-based Rituals (Shielding, Circles, Stilling/Gentling, Turning)

Date: 2026-08-18
Status: Accepted

## Context

The user pointed out a gap between the squad-abstraction principle in
`docs/game-design/07-units.md` ("one token = one abstracted squad, not an
individual") and specific Wheel of Time mechanics they wanted represented:
a single sufficiently strong Aes Sedai can Shield another (temporary), but
Stilling/Gentling a channeler takes a circle of thirteen, and turning
someone to the Shadow takes thirteen Black Ajah alongside thirteen
Myrddraal. These only make sense if the game can count exact individuals —
an abstracted squad token can't represent "thirteen of a specific kind of
person."

The user was explicit that exact canon fidelity isn't the goal here —
branching into the game's own interpretation where useful is fine and
expected.

Two follow-up questions were resolved by direct user input before this
ADR:
1. Should full rituals be attemptable mid-battle, or only as a
   post-capture strategic-layer action? **Both** — a rare, risky mid-battle
   gambit, and a safer multi-turn strategic action on a held prisoner.
2. Should turning a captured channeler to the player's side be a real
   mechanic? **Yes, but Shadow-exclusive**, via two paths: the forced
   13+13 ritual, or a strategic "Darkfriend Network" of planted agents
   inside enemy factions that can be spent on intel/resources or on
   triggering defections — framed by the user as "the Shadow's main
   resource is alliances/units."

## Decision

- **Individual-scale units are a hard representation rule, not a
  suggestion.** Channeler and Hero/Commander archetype tokens are always
  exactly one specific person — never an abstracted squad. This is the
  precondition for everything below.
- **Shielding** is a single-caster, contested, reversible action —
  matches the user's read that "later it's shown only one Aes Sedai can
  shield another if she's powerful enough."
- **Circles** let multiple channelers link and pool Power reserve through
  a leader; single-affinity by default (a house rule, not strict canon
  fidelity), with mixed-affinity circles left as a rare, unbuilt,
  campaign-unlockable idea rather than an MVP feature.
- **Rituals** are fixed-headcount, permanent-effect actions requiring a
  Circle of an exact composition around a Shielded, restrained target:
  - Stilling/Gentling: 13 same-affinity channelers (or a rare
    high-risk solo-with-sa'angreal alternate path).
  - Turning to the Shadow: 13 Black Ajah + 13 Myrddraal, Shadow-exclusive.
- Both Rituals can be attempted **mid-battle** (high risk — the whole
  circle is stationary and exposed for an extended, interruptible cast
  window) or at a **stronghold on the strategic layer** against a held
  **Prisoner** (safer, but the prisoner can be rescued in the meantime).
- **Capture** becomes a distinct battle outcome from Kill, available only
  against Shielded or broken/routing channelers, producing a Prisoner
  instead of a casualty.
- A new Shadow-exclusive strategic resource, the **Darkfriend Network**
  (planted agents in enemy territory), is the acquisition path for Black
  Ajah units and a spendable resource for intel/resources or triggering
  enemy defections — formalizing the Shadow's existing
  "wins provinces through corruption/infiltration" strategic hook into a
  concrete economic identity, per the user's stated philosophy that
  alliances are the Shadow's core resource.

## Consequences

- `docs/game-design/07-units.md` now states the individual-scale
  exception explicitly, with the rationale that it's load-bearing for
  this system, not just a modeling nicety.
- `docs/game-design/06-magic-and-channeling.md` gained a major new
  section (Shielding, Circles, and Rituals) that most future
  channeling-related work should build against.
- `docs/game-design/04-tactical-battle-layer.md` gained Shield, Capture,
  and Ritual as battle order types, and Prisoners as a battle-outcome
  category alongside kills and routs.
- `docs/game-design/05-factions.md`'s Shadow brief and
  `docs/game-design/08-economy-and-resources.md`'s resource table and
  faction-variance section were rewritten around the Darkfriend Network
  and the Turning ritual as the Shadow's defining asymmetry — the
  strongest instance yet of "no two factions play the economy the same
  way" (`docs/game-design/03-strategic-layer.md`'s stated design goal).
- `docs/game-design/09-campaign-and-progression.md` gained a Prisoners
  subsection (held status, rescue, ransom) as persistent campaign-layer
  content, not a one-battle abstraction.
- `docs/game-design/02-glossary-wot-to-game-terms.md` gained entries for
  Shielding, Circle/Linking, Turning, Capture/Prisoner, and Darkfriend
  Network, and the Black Ajah entry was updated to reflect that they're
  fieldable units once activated, not just a background subversion flag.
- Technically, `docs/technical-design/02-data-driven-content.md` gained
  Ritual as a content type with an exact-count `requires` schema shape —
  the clearest example yet in the docs of why the content/code boundary
  and the individual-scale representation rule both need to hold: a
  malformed or miscounted Ritual definition is the kind of bug that's
  invisible until a player tries to run one 26-unit ritual and it silently
  behaves wrong.
- This is a genuinely complex system for a small team to build and
  balance (contested Shielding rolls, circle-linking, interruptible
  multi-minute ritual cast windows, prisoner transport and rescue). It's
  accepted as core to the game's identity rather than deferred, but Phase
  2 prototyping should treat it as a second major risk area alongside the
  real-time-with-pause battle loop from `0002`, not an afterthought bolted
  on once the base battle loop works.
