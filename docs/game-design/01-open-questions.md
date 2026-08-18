# Open Questions — Phase 1 Decision Log

This is the working list of decisions that need a real answer before the
rest of the design docs can stop being "draft." Each entry has the
question, the options as I see them, a recommendation where I have one, and
a status. As each gets resolved, it moves to **Resolved** below with the
final answer, a one-line rationale, and a link to its ADR (see
`docs/decisions/`).

Treat this file as the front door to Phase 1: this is what "guiding you
through the process" concretely means — working down this list together.

---

## Open

### Q5. Setting anchor point in WoT continuity
- **A — A specific pre-established point** (e.g., just before *the Eye of
  the World*, or the height of the Aiel War, or the War of the Shadow).
- **B — An original "what if" period** not tied to a specific book moment,
  so faction rosters/leaders aren't constrained by canon events and the
  sandbox can diverge freely (explicitly *not* retelling the books, per the
  non-goals).

**Recommendation: B, but anchored close to the main series' status quo**
(i.e., the world as it is just before the series begins — Aes Sedai vs.
Black Ajah rumors, Seanchan not yet returned, Aiel beyond the Waste,
Trollocs raiding the Blight borders) so the setting is instantly legible to
anyone who knows the books, while the actual campaign play is a sandbox
"what really happens" rather than a scripted retelling.

---

### Q6. Strategic map scope
Is the map the whole continent (all of Randland), or a bounded region
(e.g., just the Borderlands and the Blight, or just the western nations)?

**Recommendation:** start with a bounded region for the vertical slice
(Phase 3) — small enough to fully populate with provinces/resources without
years of content work, large enough that the MVP factions
(White Tower, Whitecloaks, Aiel, Shadow — see Q4, resolved) all have a
reason to border each other. A likely first region: the Borderlands +
northern Blight edge + a slice of the central nations, since it naturally
includes Shadow incursion, a Whitecloak presence, and reachable White
Tower territory. Aiel territory borders the Waste, which may argue for
shifting the region south/west instead — worth deciding alongside actual
map layout work.

---

### Q8. IP/licensing posture
Wheel of Time is Robert Jordan's (and now Tor/Amazon's) IP. Options range
from "build entirely for personal/private use, never distribute," to
"build with clearly-filed-off names as an original setting inspired by
WoT, distributable," to "build as-is and cross the distribution bridge
later." This doesn't block Phase 1 design work, but it should be decided
before Phase 7 (release prep), and it's worth deciding your intent early
since it can affect how tightly the docs couple to WoT-specific names.

**Recommendation:** design with real WoT names/terms now (it's much easier
to design against a concrete, well-known setting than an abstracted one),
treat this as a personal/non-commercial project by default, and revisit
distribution posture explicitly before Phase 7. Flagging here so it isn't
forgotten, not because it needs resolving today.

---

## Resolved

### Q1. Battle pacing model
**Decision: Real-time with pause** (classic Total War model). The player
can pause at any time to survey the field and queue orders, then unpause
to watch them play out; combat, movement, and casting all happen on a
continuous clock rather than in discrete resolved rounds.

This was the opposite of the drafted recommendation (turn-based
simultaneous resolution), which changes both the battle-layer design and
the simulation architecture materially — see the rewritten
`04-tactical-battle-layer.md` and
`docs/technical-design/04-battle-simulation-design.md`, and
`docs/decisions/0002-real-time-with-pause-battle-pacing.md`.

### Q2. Grid geometry
**Decision: Hex grid.** Prioritizes flanking/movement feel over the extra
tooling cost. See the rewritten `04-tactical-battle-layer.md` and
`docs/decisions/0003-hex-grid.md`.

### Q4. MVP faction shortlist
**Decision: White Tower (Aes Sedai), Children of the Light (Whitecloaks),
Aiel clans, Shadow (Trollocs/Dreadlords).** Black Tower moves to the
post-MVP faction list — White Tower alone covers the "channeling as core
mechanic" slot for the vertical slice. See the updated `05-factions.md`
and `docs/decisions/0004-mvp-faction-shortlist.md`.

### Q7. Engine / tech stack direction
**Decision: Web stack — TypeScript + PixiJS.** Content ships as plain JSON
with no engine-specific import step; distribution is a browser link.
See the updated `docs/technical-design/01-tech-stack-options.md` and
`docs/decisions/0005-tech-stack-typescript-pixijs.md`.
