# Roadmap

This is a living document. Phases are sequential in emphasis, not strictly
sequential in time — e.g., art direction thinking can start during Phase 1
even though asset production doesn't happen until later.

## Phase 0 — Setup ✅

- [x] Repository created
- [x] Documentation structure established (game design / technical design /
      decisions)
- [x] Roadmap drafted

## Phase 1 — Concept & Design Bible *(current phase)*

Goal: leave this phase with a design that is internally consistent, that we
both understand equally well, and that is stable enough to prototype
against. Nothing gets built until Phase 1's core decisions are locked,
because the tactical battle layer in particular is a novel mechanic — if we
get the shape of it wrong, no amount of code quality saves it.

- [x] Resolve the highest-leverage open questions: battle pacing (real-time
      with pause), grid geometry (hex), MVP faction shortlist (White Tower,
      Whitecloaks, Aiel, Shadow), tech stack direction (TypeScript +
      PixiJS) — see `docs/decisions/0002` through `0005`
- [ ] Resolve the remaining open questions in
      `docs/game-design/01-open-questions.md` (setting anchor point,
      strategic map scale, IP/licensing posture)
- [ ] Lock the strategic layer design (`03-strategic-layer.md`)
- [ ] Lock the tactical battle layer design (`04-tactical-battle-layer.md`)
      — this is the highest-risk/highest-value doc in the project
- [ ] Lock the MVP faction list and write full faction briefs
      (`05-factions.md`)
- [ ] Lock the channeling/magic system rules (`06-magic-and-channeling.md`)
- [ ] Define the unit framework and a first-pass roster per MVP faction
      (`07-units.md`)
- [ ] Define v1 economy resources (`08-economy-and-resources.md`)
- [ ] Define campaign structure and victory conditions
      (`09-campaign-and-progression.md`)
- [ ] Write an art direction brief (palette, portrait style, UI framing —
      referencing CoE5's iconography directly)
- [ ] Sign off on the technical direction at a *decision* level (engine
      family, data-driven content approach) — not implementation yet
- [ ] Record every non-obvious decision made along the way as an ADR in
      `docs/decisions/`

**Exit criteria:** a reader who has never talked to us could read
`docs/game-design/` end to end and know exactly what game we're building,
without needing to ask "wait, how does X actually work?"

## Phase 2 — Technical Prototyping

Throwaway-code spikes to de-risk the two hardest unknowns before investing
in production architecture:

- [ ] Prototype the tactical battle grid: movement, terrain effects, order
      queue, live order-giving, combat resolution — enough to answer "is
      this actually fun and legible, or does it feel like fiddly Total War
      without the spectacle?"
- [ ] Prototype the strategic layer turn resolution with several dummy AI
      factions acting simultaneously — enough to answer "does watching
      multiple asymmetric AI factions act feel like CoE5, or does it feel
      inert?"
- [ ] Finalize engine/tech stack choice based on prototype experience, not
      just paper comparison
- [ ] Finalize the tactical/strategic data interchange (what does a
      strategic-layer army look like when it becomes a tactical battle, and
      vice versa)

**Exit criteria:** both core loops have been played, by hand, and felt good
enough to commit real production time to.

## Phase 3 — Vertical Slice

- [ ] One faction, fully playable, strategic layer → tactical battle →
      strategic layer, start to finish
- [ ] Placeholder/programmer art acceptable; systems must be real
- [ ] Save/load working
- [ ] Establish the actual project structure per
      `docs/technical-design/03-project-structure.md`

**Exit criteria:** someone who is not us can sit down and play a full,
if short, game.

## Phase 4 — Content Pipeline & Tooling

- [ ] Data schemas for factions/units/weaves/terrain/items are finalized
      and validated
- [ ] A contributor can add a new unit or faction by adding data + assets,
      without touching simulation code
- [ ] Contribution workflow documented and tested on a real addition
      (`docs/technical-design/05-contributing-guide.md`)

**Exit criteria:** adding faction #2 takes a fraction of the time faction #1
took, because it's data authoring, not engineering.

## Phase 5 — Faction & Content Expansion

- [ ] Remaining MVP factions built out to full unit rosters
- [ ] Magic system depth (full weave list, angreal/ter'angreal items,
      taint/madness consequences playing out over a campaign)
- [ ] Strategic and tactical AI behavior for non-MVP factions
- [ ] World events, random encounters

## Phase 6 — Polish, Balance, Playtesting

- [ ] Balance pass across factions
- [ ] UX pass on the battle order-giving interface specifically (this is
      the mechanic most likely to need iteration)
- [ ] External playtesting

## Phase 7 — Release Prep

- [ ] Packaging/distribution decision
- [ ] Final documentation pass
- [ ] Licensing review (Wheel of Time is Robert Jordan's/Tor's IP — decide
      early how this affects distribution; see open question in
      `docs/game-design/01-open-questions.md`)

---

### How to use this file

When a checkbox's work starts, link the relevant doc or PR next to it.
When a phase's exit criteria are met, mark the phase header ✅ and move the
"current phase" note down. Don't delete completed items — the history of
what was decided when is useful.
