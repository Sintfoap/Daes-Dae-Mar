# Magic & Channeling

> Status: Draft — core mechanic, should be one of the first systems
> validated in Phase 2 prototyping since it touches both layers.

## Design intent

Per pillar 4, channeling must be simultaneously the strongest tool in the
game and the tool with the most durable consequences for misusing it. Every
sub-system below exists to serve that tension. If a proposed weave or rule
makes channeling strictly safe, or strictly not worth the risk, it's off
pillar.

## The two halves of the Power

### Saidin (male)
- Tainted by the Dark One. Every act of channeling saidin adds to an
  accumulating **taint meter** on that channeler.
- Taint doesn't wash off. It's a one-way ratchet across a channeler's
  career (campaign-scale, not battle-scale) — this is what makes recruiting
  and fielding male channelers a long-term strategic bet, not a
  battle-to-battle stat check.
- At high taint, a channeler risks **madness**: escalating negative
  effects (unreliable weaves, erratic behavior in battle, eventually
  becoming unusable or actively dangerous to their own side). This is the
  Black Tower's defining pressure — see `05-factions.md`.

### Saidar (female)
- Untainted, but channeling beyond a channeler's safe capacity in a single
  battle risks **burnout**: a sudden, severe, often permanent loss of
  capacity if pushed too far, too fast.
- Saidar channelers can also be **stilled** (severed from the Power,
  usually as a punishment/attack mechanic rather than a self-inflicted
  risk) — a rare, campaign-altering event rather than a routine one.
- Net effect: saidar channelers are *safer to use routinely* than saidin
  channelers, but have a harder ceiling if a player tries to force one
  fight past its limits.

### The True Power (Shadow only)
- Extremely rare, extremely powerful, drawn directly from the Dark One
  rather than the Wheel's own power source.
- Reserved for a small number of hero-tier Shadow units (Forsaken-tier) —
  not a resource ordinary Dreadlords have access to. Using it should carry
  the heaviest consequences in the game, narratively and mechanically.

## Power reserve (per-battle resource)

Each channeler has a **Power reserve** that refills between battles (a
strategic-layer resource, tunable per faction/channeler strength) and is
spent weave-by-weave during a tactical battle. Running a reserve to zero
mid-battle doesn't just stop offense — for saidin users it accelerates
taint gain, for saidar users it risks burnout. This is what makes "how hard
do I push my channeler this fight" a real decision every battle, not just
a one-time strategic-layer stat.

## Weave categories

| Category | Examples | Notes |
|---|---|---|
| Offense | Fire/lightning-equivalent direct-damage weaves, up to balefire at the extreme end | Balefire should be rare, expensive, and carry unique risk (unmaking effects) — a last-resort weapon, not a spammable nuke |
| Control | Compulsion-family effects | Reserved for Shadow/Darkfriend use — using Compulsion should be treated as a moral and strategic red line even in-fiction, consistent with the books |
| Utility | Healing, Traveling/gateways, shielding | Gateways are the strategic-layer's fast-travel mechanic when available to a faction; healing matters most in prolonged campaigns |
| Detection | Sensing channeling, Foretelling-adjacent effects | Primarily strategic-layer value (see `03-strategic-layer.md`); tactically useful for revealing hidden/ambushing units |

A channeler's available weave list should be a function of **faction +
individual strength/training tier**, not a universal spell list every
channeler can pick from — an Aes Sedai Green and a Dreadlord shouldn't have
the same options even where their raw categories overlap.

## Relics

- **Angreal / sa'angreal:** amplify a channeler's effective strength —
  modeled as equipment that raises Power reserve and/or weave strength.
  Rare, strategic-layer resources (see `08-economy-and-resources.md`).
- **Ter'angreal:** fixed, specific effects rather than raw amplification —
  modeled as unique items/abilities, not a stat boost. Each one is
  effectively a small, bespoke rule, which is intentional — it's where
  flavorful one-off mechanics belong instead of bloating the general
  weave list.

## Detecting and countering channelers

Non-channeling factions (Whitecloaks especially) need real tools against
channelers, or "field a channeler" becomes a dominant strategy with no
answer. Recommended tools, to be detailed once Phase 2 validates the
combat model:
- Specialized anti-channeler units/relics (drawing on Whitecloak
  lore/tools) that impose penalties on enemy channelers or ignore some of
  their defenses.
- Focus-fire viability: channelers should be identifiable, targetable, and
  meaningfully more fragile than front-line infantry if actually reached
  in melee — the tactical answer to a channeler is often "kill it before
  it acts," which requires the battle layer to make that a real, visible
  option (see `04-tactical-battle-layer.md`'s cast-step "tell").

## Open items

- Exact taint/burnout accumulation curves — a balance question for Phase 6,
  not a Phase 1 blocker, but the *shape* (one-way ratchet for taint,
  spike-risk for burnout) should be locked now since it affects faction
  identity.
- Full weave list per faction/tier — belongs alongside each faction's unit
  roster work in `07-units.md`.
- Whether stilling/gentling is purely a narrative/event-driven outcome or
  a battlefield-achievable one (e.g., a rare ability that can gentle/still
  an enemy channeler mid-campaign) — flagged for a design discussion, not
  yet recommended either way.
