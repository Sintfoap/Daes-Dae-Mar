# 0009. White Tower's political system: Ajah Lean, Favor, succession, and alliance-driven recruitment

Date: 2026-08-18
Status: Accepted

## Context

Continuing the White Tower deep-dive, the user wanted the faction's
identity pushed further toward "mainly political" — alliances as the
route to disposable units and income, a win condition that reflects that,
new rituals for power/units beyond the existing Stilling/Turning pattern,
and a concrete Ajah mechanic. On the Ajah question specifically, the user
proposed tying the Ajah specialization to whichever Ajah the sitting
Amyrlin Seat came from (citing Siuan Sanche favoring the Blue Ajah as
Amyrlin), with a bonus to that Ajah and a detriment to an opposed one —
rather than a static player choice made once at campaign start.

Three questions were resolved by direct user input before this ADR:
1. Ajah model: **hybrid** — one faction, an Ajah Lean specialization, plus
   internal Ajah-favor politics — refined per the Amyrlin-tied mechanic
   above rather than a static campaign-start pick.
2. Conquest viability: **political is the main path, conquest stays
   viable** — not mechanically forced.
3. Oath Rod scarcity: **single unique copy** on the whole map.

## Decision

- The **Ajah Lean** is derived from the current Amyrlin Seat's home
  Ajah, not chosen once at setup. Losing/replacing the Amyrlin can change
  the Lean.
- Each Ajah has a **Favor** meter; the Lean raises the home Ajah's Favor
  and lowers a paired rival Ajah's (first-pass pairings: Blue↔Red,
  Green↔Brown, White↔Gray, Yellow largely neutral) — adjustable, not
  locked.
- A rival Ajah with critically low Favor becomes a preferential target for
  the Shadow's Darkfriend Network (`08-economy-and-resources.md`) — ties
  White Tower's internal politics directly to an existing Shadow mechanic
  rather than inventing a parallel one.
- Overall **Unity** (aggregate Favor imbalance) gates a **Tower schism**
  failure state, and a badly resolved **succession** (contested, or
  occurring while Unity is already low) can trigger one directly — the
  Tower splits into two rival Amyrlins rather than resolving cleanly.
- **Recruitment runs through alliances**: allied nations send novices
  (feeding the Aes Sedai training pipeline) in addition to gold tribute
  and borrowed levies. A bigger alliance network compounds — more
  alliances, faster long-term growth, not just more immediate resources.
- **Win condition**: "Unite the Bound" — win via alliance-coverage of the
  map past a threshold (weighted toward Oath-bound alliances), or by
  leading the largest coalition at the campaign's endgame clock
  (`09-campaign-and-progression.md`).
- New rituals, deliberately kept separate from the 13-channeler
  Stilling/Turning pattern: **Binding Oath** (the singular Oath Rod makes
  a willing alliance permanently unbreakable), **Gateway Network**
  (semi-permanent Traveling link between two provinces), **Tower Ward**
  and **Mass Healing** (smaller, Ajah-lean-flavored circle-workings).

## Consequences

- `docs/game-design/05-factions.md`'s White Tower entry gained a
  substantial "Internal politics: the Ajah Lean" and "New rituals"
  treatment — noticeably longer than other factions' briefs, which is
  appropriate given this is the faction under active deep design, not a
  precedent every faction needs matched immediately.
- The Amyrlin Seat (`07-units.md`) is now load-bearing for a faction-wide
  mechanic, not just a flavorful unique hero — protecting her, and
  managing who's positioned to succeed her, is real strategic content.
- The Oath Rod is the first named, singular relic in the setting with a
  mechanical effect specified before the general relic system
  (`docs/decisions/0010-relic-equipment-system.md`) was written — the two
  should stay consistent as that system firms up.
- Real open items, deliberately left for later: exact Favor/Unity
  numbers and decay rates (Phase 6 balance pass); the exact succession
  resolution formula (Favor-weighted lottery vs. player-driven contest vs.
  hybrid); whether a forced (unwilling) Binding Oath is actually built as
  a playable dark option or stays a narrative threat associated with the
  Shadow stealing the Rod.
- This is a meaningfully more complex internal-politics system than any
  other MVP faction has. Accepted deliberately, matching the user's
  stated direction that White Tower's whole identity should be political,
  but worth flagging for Phase 2 scoping alongside the other
  already-identified complexity risks (real-time-with-pause battles,
  headcount rituals).
