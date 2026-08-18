# Economy & Resources

> Status: Draft — v1 proposal, deliberately kept close to CoE5's simple
> resource model rather than a deep economic simulation.

## Design intent

CoE5 runs on a small number of resources (gold, a secondary resource or
two, magic sites) rather than a sprawling economic web — that's part of
why it can support so many factions without each one needing a bespoke
economy. This project should follow that lead: enough resource variety to
make faction identity and strategic decisions real, not so much that the
strategic layer turns into spreadsheet management.

## Proposed v1 resources

| Resource | Represents | Primary use |
|---|---|---|
| **Gold** | General wealth | Recruiting most units, upkeep, buildings |
| **Food** | Provisioning | Army upkeep on campaign, siege attrition, growth |
| **Influence** | Political capital, renown | Faction-specific: White Tower recruitment/politics, diplomacy, hero recruitment |
| **Taint / Corruption** | Accumulated cost of channeling saidin or Shadow corruption | Not spent — a rising liability tracked per-channeler and, for the Shadow, potentially per-province (Blight spread) |
| **Relics** (angreal/sa'angreal/ter'angreal) | Rare magical items | Equipment-slot resource for channelers; acquired, not manufactured, in most cases |

Four spendable resources plus one liability-resource is intentionally
close to CoE5's own scope. Resist adding a sixth spendable resource
without a clear faction-identity reason — see the strategic-layer note in
`03-strategic-layer.md` about every faction needing genuinely different
priorities among the *same* resource set, rather than each faction getting
its own bespoke currency.

## Why Taint/Corruption is a resource and not just a stat

Treating it as a tracked resource (rather than a hidden number) makes it
visible and plannable — the player should always be able to see "this
channeler is at X taint, here's roughly what that means" the same way they
can see their gold total. It's a resource that only goes up (for a given
channeler, saidin side) or spikes (saidar burnout), which is unusual and
worth calling out explicitly in any resource-system code/UI work later —
see `docs/technical-design/02-data-driven-content.md`.

## Faction variance in resource use

Per the strategic-layer design goal that no two factions play the same:

- **White Tower:** Influence-heavy; can achieve strategic goals by
  spending Influence instead of moving armies.
- **Seanchan:** Converts captured enemy channelers into a resource
  (damane) rather than paying Relic-equivalent costs for channeling power
  — a unique acquisition path, not just a discount.
- **Shadow:** Corruption doubles as an offensive strategic tool (spreading
  Blight/subversion into enemy provinces), not just a per-channeler
  liability.
- **Aiel:** Low Gold/Food dependency relative to settled nations (raiding
  and clan support rather than province economies), high dependency on
  Influence-equivalent (honor/clan standing) instead.

## Open items

- Exact yield/cost numbers per province terrain type and per unit — a
  balance pass, not a Phase 1 blocker.
- Whether Relics are ever "manufactured" (crafted) versus purely
  found/looted/inherited — recommend purely acquired for MVP, matching how
  rare these items are in the source material; revisit only if a faction's
  identity seems to need crafting.
- Trade/market mechanics between factions — explicitly out of scope for
  MVP per the diplomacy note in `03-strategic-layer.md`; revisit post
  vertical-slice if it's missed.
