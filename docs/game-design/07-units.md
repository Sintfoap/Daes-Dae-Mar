# Units

> Status: Draft — framework only. Full rosters populate per-faction as
> each faction enters the build queue (see `05-factions.md` checklist).

## Unit archetypes

Every unit in the game, regardless of faction, is built from one of these
archetypes. Archetypes exist so the tactical battle layer's rules
(`04-tactical-battle-layer.md`) only need to reason about a handful of
behavioral categories, even as the faction roster grows large.

| Archetype | Battlefield role | Example |
|---|---|---|
| Line infantry | Holds ground, anchors formations | Whitecloak men-at-arms |
| Skirmisher / ranged | Damage at range, weak in melee | Aiel bowmen, Seanchan archers |
| Shock cavalry | Fast, strong charge bonus, weak sustained melee | Borderlander lancers |
| Channeler | High-impact weaves, fragile, resource-limited (see `06-magic-and-channeling.md`) | Aes Sedai, Asha'man, Dreadlord, damane |
| Hero / commander | Unique named unit, morale anchor, often has a special ability | A named Aiel clan chief, a Forsaken |
| Beast / shadowspawn | Non-human, often faction-exclusive rules | Trolloc, raken, grolm |
| Siege | Slow, specialized against fortifications | Trebuchet-equivalent, breaching tools |

A given faction typically fields 4–7 archetypes with faction-specific
flavor, not all 7 — the Aiel notably field no shock cavalry at all, which
is itself a piece of faction identity (see `05-factions.md`).

## Stat template

Every unit's stat block should cover, at minimum:

- **Strength/HP** — how much punishment the unit (as an abstracted
  squad/company, not an individual) can take
- **Attack** — melee and/or ranged offense
- **Defense** — mitigation, separate from HP
- **Move** — grid cells per order
- **Morale** — baseline resistance to routing (see
  `04-tactical-battle-layer.md`)
- **Special tags** — flags like *cannot be flanked from forest*, *ambush
  bonus*, *fear aura*, *channeler (see weave list)*, *no cavalry counter*,
  etc. — this is where most of a unit's actual personality lives, more
  than in the raw numbers

## Representation and scale

Per Q3 in `01-open-questions.md`: one grid token represents an abstracted
squad/company of soldiers (CoE5-style single-icon-per-unit), not an
individual combatant, for most archetypes. Strength/HP represents the
unit's remaining fighting power as a whole, not hit points on one body.

**Exception — individual-scale units.** Channeler and Hero/Commander
archetype tokens are never abstracted squads: **one token is exactly one
specific, named person**, always. This is a deliberate carve-out from the
squad abstraction above, and it's load-bearing, not cosmetic: several of
the setting's signature magic mechanics — Shielding, Circles, and the
Stilling/Gentling and Turning rituals (`06-magic-and-channeling.md`) —
depend on the game being able to count exact numbers of exact individuals
present and linked. "A circle of thirteen Aes Sedai" only means something
if the simulation can verify thirteen distinct Channeler tokens of the
right type are on the field and linked together — it can't be represented
by thirteen soldiers inside one abstracted squad icon. Line
infantry/cavalry/beasts stay abstracted; channelers and named heroes never
are.

## Example unit cards (illustrative, not final)

**Whitecloak Man-at-Arms** (Children of the Light, Line infantry)
- Solid stats across the board, formation bonus when adjacent to another
  Whitecloak infantry unit, no special vulnerability to Compulsion/fear
  effects (unwavering faith) but no channeling counter-tools baseline —
  those come from separate specialist units.

**Aiel Spear (Warrior Society)** (Aiel, Line infantry / skirmisher hybrid)
- Below-average Defense but above-average Attack and Move; large bonus in
  forest/hill terrain; morale penalty when fighting in open ground away
  from cover — mechanically pushes the player toward choosing terrain
  deliberately, per pillar 3.

**Asha'man Soldier** (Black Tower, Channeler)
- Small Power reserve relative to full Aes Sedai, but can also fight
  competently in melee (unlike most channeler units) — reflects the
  Black Tower's martial-first training; gains taint per weave cast, with a
  visible taint-meter tracked across the campaign, not just the battle.

**Damane (handled)** (Seanchan, Channeler — unique pairing rule)
- Strong ranged-weave offense but must remain within a short range of its
  paired sul'dam handler unit or suffers major penalties/becomes
  uncontrollable — makes protecting (or targeting) the handler a real
  tactical thread distinct from any other channeler unit in the game.

## Worked example: White Tower's roster shape

White Tower was the first faction to get real balancing scrutiny
(`docs/decisions/0008-white-tower-warder-tiers.md`), because an army built
entirely from individual-scale Channeler tokens runs into a hard problem:
per the Representation and scale rule above, every one of those tokens is
exactly one person, while an opposing faction's army is mostly squad-scale
companies. Same token count, wildly mismatched actual manpower — bad for
the fiction and bad for balance (fragile individuals need absurd per-token
stats to not just evaporate against a company).

The fix is that **Warders exist at two tiers**, not one, and White
Tower's roster is built in layers of rising cost and fragility:

**Tower Guard** (Line infantry, squad-scale)
- Cheap, fast to recruit, unremarkable stats — ordinary city levies and
  Tower staff-at-arms. Board presence and a first line to absorb early
  losses, so Warder Companies aren't spent as disposable meat shields.

**Warder Company** (Line infantry, squad-scale, elite tags)
- An organized body of trained Warders operating as a military unit — not
  tied to any specific Aes Sedai. Better stats than Tower Guard and than a
  typical faction's basic line infantry (Warder training is exceptional),
  costed and recruited accordingly. This is White Tower's actual
  line-holding answer — the "main infantry" the roster is built around.

**Aes Sedai** (Channeler, individual-scale)
- Recruited (slowly — see the training-pipeline question in
  `10-faction-deep-dive.md`) rather than trained instantly like a company.
  Fragile in melee, powerful at range/weaves, expensive relative to a
  whole Warder Company. The precious, protected core of the army.

**Bonded Warder** (Hero/Commander, individual-scale — an *optional
upgrade*, not a default)
- A specific Warder personally bonded to a specific Aes Sedai, purchased
  as a strategic-layer upgrade on an existing Aes Sedai unit rather than
  something every channeler starts with — keeps bonded pairs rare and
  meaningful instead of mandatory overhead on every Aes Sedai token.
  Grants real mutual combat/defense bonuses while both live, and a real
  mutual-loss penalty if either half dies, is captured, Stilled, or the
  bond is otherwise severed — protecting a bonded pair should read as
  higher-stakes than protecting either half alone.

**Composition target** (a Phase 2/6 number to pressure-test, not a locked
formula): a well-built White Tower army should skew **majority Tower
Guard/Warder Company tokens, with Aes Sedai as a well-protected
minority** — roughly 60–70% mundane/elite-mundane to 20–30% actual
channelers is a reasonable starting target. The point isn't the exact
split; it's that White Tower should *not* read as an all-caster army by
token count, even though the caster minority is where the interesting
decisions live. Terrain matters here too: a channeler backline on a hill
behind a Warder Company screen (per the deployment trade-offs in
`04-tactical-battle-layer.md`) is the intended default shape of a White
Tower deployment, not an incidental one.

## Heroes and named units

Ta'veren, Wolfbrothers, Forsaken, clan chiefs, and similar named
individuals are Hero/Commander archetype units with:
- A unique ability not available to generic units of their type
- A morale-anchor effect on nearby friendly units
- Campaign-persistence — heroes can be lost permanently (death, capture,
  stilling/gentling) with real strategic consequences, which is what makes
  them worth protecting rather than just strong stat sticks

Full hero design (leveling, acquisition, loss consequences) belongs in
`09-campaign-and-progression.md`.

## Open items

- Full per-faction rosters — populated as each faction is greenlit (see
  `05-factions.md` build-queue checklist)
- Exact numeric balancing — a Phase 6 concern, not a Phase 1 blocker
- Whether unit *upgrades* exist generally (a unit gaining equipment/
  veterancy over a campaign) beyond the Bonded Warder precedent above —
  still deferred to `09-campaign-and-progression.md` as a
  campaign-structure question, but the Bonded Warder upgrade shows the
  pattern works for at least one case
- Exact cost/time numbers for the Aes Sedai training pipeline and Bonded
  Warder upgrade cost — Phase 6 balance pass; tracked alongside the White
  Tower composition target above
