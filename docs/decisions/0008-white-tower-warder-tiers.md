# 0008. White Tower fields two Warder tiers to avoid an all-individual-scale army

Date: 2026-08-18
Status: Accepted

## Context

The user raised a balance concern while starting the White Tower
deep-dive (`docs/game-design/10-faction-deep-dive.md`): White Tower's
roster, as briefed, was effectively "Aes Sedai plus their Warders," and
per the individual-scale representation rule (ADR 0007), every one of
those tokens is exactly one person. Every other faction's army is mostly
squad-scale companies (dozens/hundreds of soldiers abstracted per token).
Same token count, wildly mismatched manpower — which breaks the fiction of
a fair fight and forces individual-scale tokens toward absurd per-unit
power to avoid simply evaporating against a company.

The user liked the instinct that Warders should be White Tower's main
infantry, but wanted that idea actually balanced rather than assumed.

Two follow-up questions were resolved by direct user input:
1. Should the Aes Sedai–Warder bond be a default most Aes Sedai have, or a
   rare optional upgrade? **Optional upgrade.**
2. Should there be a separate cheap Tower Guard filler tier below Warder
   Companies? **Yes.**

## Decision

White Tower's roster is built in four layers instead of one
undifferentiated "Aes Sedai + Warder" pair:

1. **Tower Guard** — cheap, fast, squad-scale line infantry filler.
2. **Warder Company** — squad-scale, elite-tagged line infantry; an
   organized body of trained Warders acting as a military unit, not tied
   to a specific Aes Sedai. This is the actual "Warders as main infantry"
   answer, given real board presence by being squad-scale.
3. **Aes Sedai** — individual-scale Channeler unit, recruited slowly and
   expensively relative to the tiers above.
4. **Bonded Warder** — an optional strategic-layer upgrade attaching a
   specific, individual-scale Warder to a specific Aes Sedai, with real
   mutual bonuses and a real mutual-loss penalty. Not a default; a
   deliberate investment.

Target composition (a number to pressure-test, not a locked formula):
roughly 60–70% of a White Tower army's tokens should be Tower
Guard/Warder Company, 20–30% actual Aes Sedai — an army with a mundane
majority and a precious, protected caster minority, not an all-caster
army.

## Consequences

- `docs/game-design/07-units.md` gained a "Worked example: White Tower's
  roster shape" section laying out all four tiers and the composition
  target — the first faction to get this level of roster detail, and a
  template other factions' deep-dives can follow when they hit similar
  scale questions (Seanchan's damane/sul'dam pairing and Shadow's
  Trolloc-band-vs-Dreadlord split are likely candidates).
- The Bonded Warder upgrade is the first concrete instance of the
  "unit upgrade" pattern flagged as an open question in `07-units.md` —
  doesn't resolve that question generally, but shows the pattern works for
  at least one real case.
- `docs/game-design/10-faction-deep-dive.md`'s White Tower §1 and §3
  questions (roster wishlist, how thin the roster should be) are answered
  by this ADR rather than left open.
- Exact recruitment costs, training-pipeline duration, and Bonded Warder
  upgrade cost are still open numeric questions — Phase 6 balance pass,
  same as every other faction's numbers — but the *shape* (four tiers,
  rough composition target) is locked now since it determines how the
  roster and recruitment UI need to be structured.
