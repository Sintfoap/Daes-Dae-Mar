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
| **Relics** (angreal/sa'angreal/ter'angreal) | Rare magical items | Equipment-slot resource for Hero/Commander units — angreal/sa'angreal channeler-gated, ter'angreal usable by any Hero/Commander (see `06-magic-and-channeling.md` and `docs/decisions/0010-relic-equipment-system.md`); acquired, not manufactured, in most cases |
| **Darkfriend Network (Agents)** — Shadow-exclusive | Sleeper agents planted inside enemy provinces/factions | Cashed in for intelligence/resources, or spent to trigger an enemy unit or province defection event; the acquisition path for Black Ajah specifically (see below) |

Four spendable resources plus one liability-resource, common to every
faction, is intentionally close to CoE5's own scope. Resist adding a
universal sixth spendable resource without a clear faction-identity
reason — see the strategic-layer note in `03-strategic-layer.md` about
every faction needing genuinely different priorities among the *same*
resource set, rather than each faction getting its own bespoke currency.

The Darkfriend Network is the deliberate exception, and it's
faction-exclusive rather than universal for exactly that reason: the
Shadow's whole strategic identity (`05-factions.md`) is that its provinces
and units come from turned people rather than gold or conquest — "the
Shadow's main resource is alliances," not a sixth generic currency every
faction shares. See `06-magic-and-channeling.md`'s Turning ritual for the
mechanic this resource ultimately feeds: a well-developed network inside
an enemy faction (the White Tower, most notably) is how the Shadow
acquires the Black Ajah units a Turning circle requires in the first
place.

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

- **White Tower:** Influence-heavy, and recruitment itself runs through
  alliances rather than Gold alone — allied nations send novices into the
  training pipeline on top of tribute and borrowed levies
  (`docs/decisions/0009-white-tower-political-system.md`), so growing the
  alliance network compounds into growing the Tower's own future roster,
  not just immediate income. Internally, per-Ajah **Favor** functions as
  a political sub-resource feeding the faction's Unity/schism risk.
- **Seanchan:** Converts captured enemy channelers into a resource
  (damane) rather than paying Relic-equivalent costs for channeling power
  — a unique acquisition path, not just a discount.
- **Shadow:** Corruption doubles as an offensive strategic tool (spreading
  Blight/subversion into enemy provinces), not just a per-channeler
  liability; and unlike every other faction, its primary path to *both*
  new provinces and new channeler units runs through the Darkfriend
  Network above rather than through Gold/recruitment — a deliberate
  inversion of how the rest of the roster plays the economy.
- **Aiel:** Low Gold/Food dependency relative to settled nations (raiding
  and clan support rather than province economies), high dependency on
  Influence-equivalent (honor/clan standing) instead; also sits on
  unusually relic-rich territory (`docs/decisions/0010-relic-equipment-system.md`),
  giving other factions a reason to court Aiel access even though Aiel
  custom keeps most Aiel from using what they find themselves.

## Prisoners are a status, not a resource

Captured channelers (`06-magic-and-channeling.md`'s Capture battle
outcome) are tracked as a **unit status** — held at a stronghold/province —
rather than as a spendable resource. They matter economically only as the
precondition for the Stilling/Gentling and Turning rituals: holding one is
what makes the required 13- or 13+13-channeler roster worth assembling.
Guarding and potentially rescuing prisoners is real strategic-layer
content (see `09-campaign-and-progression.md`), not an economy mechanic in
its own right.

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
