# Open Questions — Phase 1 Decision Log

This is the working list of decisions that need a real answer before the
rest of the design docs can stop being "draft." Each entry has the
question, the options as I see them, a recommendation where I have one, and
a status. As each gets resolved, move it to the bottom under **Resolved**
with the final answer and a one-line rationale, and update the doc(s) it
affects.

Treat this file as the front door to Phase 1: this is what "guiding you
through the process" concretely means — working down this list together.

---

## Open

### Q1. Battle pacing model
How does the player actually give orders during a tactical battle?

- **A — Real-time with pause** (classic Total War). Battle runs
  continuously; player can pause at any time to survey and queue orders,
  then unpause. Tense, immediate, rewards fast reads.
- **B — Turn-based, simultaneous resolution.** Each side plans a round of
  orders, then both execute at once (like old-school tactics games, or
  CoE5's own turn structure extended into battle). Calmer, more deliberate,
  easier to reason about exactly what will happen.
- **C — Turn-based, alternating.** Player acts, then enemy acts, like a
  standard tactics/roguelike. Simplest to build and to read, but can feel
  static compared to a "battle."

**Recommendation: B.** It keeps the "thinking person's battle" pillar
intact (no reflex pressure), fits a grid better than real-time does (grid
combat resolved in real time tends to look janky — units sliding
tile-to-tile on a clock), and is the more natural extension of CoE5's own
turn-based DNA than bolting on Total War's real-time engine would be. It
also composes better with channeling: weaves that need a beat of "cast time
that can be interrupted" are much easier to make legible turn-by-turn than
in real time.

**This is probably the single highest-leverage decision in the whole
project** — it determines the shape of `04-tactical-battle-layer.md` and a
large fraction of the technical architecture. Worth deciding first.

---

### Q2. Grid geometry
- **A — Square grid.** Simple, matches the "bottom-to-top lanes" framing
  well, easiest to reason about and to build tooling for.
- **B — Hex grid.** Better movement/flanking feel (no diagonal-distance
  weirdness), standard for tactics games, slightly more complex UI and
  pathfinding.

**Recommendation: A (square).** The pitch emphasizes CoE5-style visual
simplicity; square grids read more like CoE5's own presentation and are
easier to pair with rectangular terrain features (river crossings, wall
segments, forest blocks) that come straight out of a map. Hex grids shine
most when 6-directional movement itself is a tactical feature, which isn't
core to this pitch.

---

### Q3. Battlefield scale and unit representation
How many "things" does the player actually control in one battle?

- Roughly how large is a deployment zone (rows/columns)?
- Does one grid token represent an individual soldier, a small squad, or a
  full company (CoE5 represents a whole unit as one icon)?

**Recommendation:** one token = one unit (a company/squad of many soldiers
abstracted as a single fighting strength, CoE5-style), not individual
soldiers. A battle should be maybe 8–20 tokens per side at MVP scale —
enough for real formation and flanking decisions, not so many it becomes a
spreadsheet. Battlefield perhaps 9–13 columns wide by 14–20 rows tall
(taller than wide, to give the bottom-to-top advance room to matter).

---

### Q4. MVP faction shortlist
The full faction list (`05-factions.md`) will eventually be large. Which
3–4 factions get built first for the vertical slice (Phase 3)? They should
be chosen to maximize how *different* their playstyles are, to prove the
framework generalizes early rather than late.

**Recommendation (placeholder, needs your call):** one channeling-heavy
faction (White Tower or Black Tower), one anti-channeling martial faction
(Children of the Light or a Borderland nation), one Shadow faction
(Trollocs/Dreadlords), and one terrain/skirmish specialist (Aiel). That
spread exercises: magic-as-core-mechanic, magic-as-threat-to-defend-against,
horde/attrition play, and terrain-dependent play — four very different
tactical-layer experiences from one framework.

---

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
years of content work, large enough that the MVP factions all have a
reason to border each other. Expand the map in Phase 5 alongside faction
expansion. A likely first region: the Borderlands + northern Blight edge +
a slice of the central nations, since it naturally includes Shadow
incursion, Borderland defenders, and reachable White Tower/Black Tower
territory.

---

### Q7. Engine / tech stack direction
This only needs a *direction*, not a final commitment (Phase 2 prototyping
will validate it). See `docs/technical-design/01-tech-stack-options.md` for
the actual tradeoff writeup — this entry just tracks that a decision is
pending and needs your input, since it has real workflow implications
(what languages you'll be reading/writing, how content gets authored, how
it gets distributed).

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

*(none yet)*
