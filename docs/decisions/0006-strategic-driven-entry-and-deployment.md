# 0006. Battle entry edge driven by strategic attack direction; asymmetric deployment freedom

Date: 2026-08-18
Status: Accepted

## Context

The original tactical battle design (`docs/game-design/04-tactical-battle-layer.md`,
prior to this decision) used a fixed axis: the player always entered from
the battlefield's south edge, the enemy always from the north, regardless
of where the attack actually came from on the strategic map. Deployment
was described as "typically the southern 2-4 rows" for whichever side was
being controlled, with no asymmetry between attacker and defender.

This was simple and legible, but it left two things on the table that the
user specifically wanted:
1. A battle's orientation should reflect the actual geography of the
   strategic-layer attack that caused it, not an arbitrary fixed screen
   direction.
2. Deployment should carry real, terrain-linked trade-offs — not just
   "arrange your units somewhere in a zone," but choices with matched
   upside and downside (hold a hill vs. stay flexible, concentrate at a
   chokepoint vs. spread to cover multiple lanes, etc.).

## Decision

- The **attacker's entry edge** on the tactical hex battlefield is
  determined by the direction of the strategic-map province the attack
  came from, not a fixed axis. A province attacked from its western
  neighbor is entered from the west edge of the battlefield; from the
  north, the north edge; and so on.
- **Deployment is asymmetric.** The attacker deploys within a bounded band
  adjacent to their entry edge (a "beachhead"). The defender deploys
  across most of the rest of the battlefield (excluding a small buffer
  near the attacker's entry edge) — reflecting that the defender is
  fighting on ground they already hold and gets more freedom to choose
  how to use it.
- **Terrain-linked deployment trade-offs** are made explicit as a design
  pattern (hold a hill for a defense bonus vs. a worse retreat if routed;
  concentrate at a chokepoint vs. spread across lanes; etc.), and should
  be implemented as terrain/unit tags in data
  (`docs/technical-design/02-data-driven-content.md`), not hardcoded
  per-case logic.
- The strategic layer's province adjacency needs to carry **direction**,
  not just an adjacency flag — see the new Q9 in
  `docs/game-design/01-open-questions.md` for the still-open question of
  exactly how that's modeled (most likely, provinces as hex tiles at the
  strategic scale, for a clean six-direction mapping onto the battle
  grid's six edges).

## Consequences

- `docs/game-design/04-tactical-battle-layer.md` was rewritten: the fixed
  "bottom-to-top" orientation section became a strategic-attack-driven
  entry-edge section, and the deployment phase section was rewritten
  around asymmetric zones and a terrain trade-off table.
- `docs/game-design/00-pillars-and-pitch.md` and `README.md` had their
  fixed-orientation language updated to match.
- `docs/game-design/03-strategic-layer.md` now specifies that province
  borders carry direction, and notes that this naturally supports
  multiple attacking forces converging on the same province from
  different edges — flagged as a Phase 5+ enhancement, not required for
  MVP, but not requiring a redesign to add later either.
- Technically, this pushes real complexity into the presentation layer
  rather than the simulation: `docs/technical-design/04-battle-simulation-design.md`
  now specifies that the simulation stays orientation-agnostic internally
  (always resolving against a canonical "attacker enters from here"
  direction), while rendering/camera/UI handle rotating that into the
  direction the player actually attacked from. This is a deliberate
  choice to keep simulation logic simple and correct for any entry edge,
  at the cost of a rendering-layer rotation step that Phase 2 needs to
  validate feels right (e.g., does the camera/UI genuinely read clearly
  when a battle is oriented east-to-west instead of south-to-north?).
- Deployment zone computation (attacker beachhead vs. defender
  everything-else) needs to be a pure function of the entry edge and
  board shape, not a hand-authored shape per battle — flagged in the
  updated technical doc.
- `docs/decisions/0003-hex-grid.md`'s consequences section referenced the
  now-superseded fixed south/north framing and was corrected to point
  here.
