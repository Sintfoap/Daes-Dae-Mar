# 0004. MVP faction shortlist

Date: 2026-08-18
Status: Accepted

## Context

`docs/game-design/01-open-questions.md` Q4 needed a resolved answer for
which factions get built first for the Phase 3 vertical slice. The
drafted recommendation was White Tower, Black Tower, Children of the
Light, and Aiel — chosen to spread across "magic as core mechanic," "magic
as threat to defend against," and "terrain-dependent play," while
deliberately deferring the Shadow (a strategically distinct
infiltration/horde playstyle, per `docs/game-design/03-strategic-layer.md`
and `05-factions.md`) to a later phase.

## Decision

MVP factions are: **White Tower (Aes Sedai), Children of the Light
(Whitecloaks), Aiel clans, and Shadow (Trollocs/Dreadlords).** Black Tower
moves to the post-MVP faction list.

## Consequences

- White Tower alone covers the "channeling as core mechanic" slot for the
  vertical slice — Black Tower's distinguishing traits (saidin taint
  pressure, martial-first channelers) are deferred to Phase 5, so the MVP
  doesn't validate the taint/madness mechanics from
  `docs/game-design/06-magic-and-channeling.md` as directly as the drafted
  shortlist would have. Worth keeping in mind when Phase 2/3 prototyping
  checks whether the channeling risk/reward loop actually lands — it may
  be under-exercised until Black Tower is built.
- The MVP set now includes the Shadow's infiltration/subversion strategic
  hook and its horde/attrition tactical hook from the start, which is a
  meaningfully different (and higher-value) spread for proving the
  strategic layer's "every faction is a real player" pillar
  (`docs/game-design/00-pillars-and-pitch.md`) than the drafted set was —
  it adds a faction that can win provinces without fighting a battle at
  all, which is a good early stress-test of that system.
- `docs/game-design/05-factions.md` was reordered so these four are the
  clearly-marked MVP set.
