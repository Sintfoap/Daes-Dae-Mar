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
| Utility | Healing, Traveling/gateways | Gateways are the strategic-layer's fast-travel mechanic when available to a faction; healing matters most in prolonged campaigns |
| Shielding / Circles / Rituals | Shield, Link, Stilling/Gentling, Turning | Their own subsystem, not a generic weave list entry — see "Shielding, Circles, and Rituals" below |
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

## Shielding, Circles, and Rituals

**Decision (`docs/decisions/0007-headcount-rituals.md`):** single powerful
channelers can Shield another — temporarily, reversibly — but the deeper,
permanent interventions (Stilling/Gentling, and Turning someone to the
Shadow) take a precise number of channelers acting together. This project
runs with that distinction as a real mechanic, not flavor text, branching
from canon specifics where it serves the game better (noted inline below)
rather than trying to reproduce the books exactly.

This is also the concrete reason individual-scale units (Channelers,
Heroes/Commanders) are never abstracted into squad tokens
(`07-units.md`'s Representation and scale) — these mechanics only mean
something if the game can count exact people.

### Shielding — single-caster, reversible
- Any channeler above a strength/skill threshold can attempt to Shield
  another channeler: a weave that cuts the target off from the Power
  without harming them.
- Resolved as a **contested check** between caster and target strength —
  not guaranteed. The stronger the caster relative to the target, the more
  likely (and more durable) the shield.
- Reversible: the target's own side can Release a shield with another
  channeler, or it can lapse naturally over time.
- Tactically, this is the fast, cheap answer to an enemy channeler
  mid-battle — neutralize their weaves without needing to kill them — at
  the cost of the caster's own Power reserve and a moment of the caster's
  own vulnerability while shielding.
- Shielding a target is normally the **prerequisite** for the Rituals
  below — you generally can't run a Stilling/Gentling or Turning circle on
  someone still free to channel back at you.

### Circles — linking multiple channelers
- Multiple channeler units can **Link** into a Circle: one acts as leader,
  the rest contribute their Power reserve to the leader's pool for the
  duration of the link.
- A linked circle can cast weaves beyond any single member's individual
  capacity, and is the structure that makes the fixed-headcount Rituals
  below possible at all.
- **House rule (branching from canon):** circles are single-affinity
  (saidar-only or saidin-only) by default, matching the setting's baseline
  limit. A mixed-affinity circle is treated as an extremely rare,
  campaign-unlockable event (a relic or a story beat, echoing Rand and
  Nynaeve's breakthrough) rather than a standard tactical option — see
  Open items.
- Linking takes time (a cast-step, interruptible like any weave) and holds
  every linked unit stationary and vulnerable for its duration — a circle
  is powerful but a highly visible, highly targetable commitment, which is
  what keeps it from being a free upgrade.

### Rituals — fixed headcount, permanent effect
Rituals are the highest-stakes actions in the game: slow to assemble,
unmissable while in progress, and permanent when they succeed. Two are
defined at MVP.

**Stilling / Gentling** — permanently severing a channeler from the Power.
- **Default path:** a Circle of **13 same-affinity channelers** (13 Aes
  Sedai, or 13 Black Tower channelers) linked around a restrained target.
- **Alternate path (house rule):** a much smaller link — as few as one
  channeler — wielding a sufficiently powerful sa'angreal can attempt it
  alone, at significantly higher backlash risk on failure. Meant to be
  rare and dramatic (a Choedan-Kal-scale moment), not a routine shortcut
  around recruiting thirteen channelers.
- The target must already be unable to resist: **Shielded** and
  captured/restrained, not freely channeling.
- Requires an extended, uninterruptible cast window. Breaking the circle
  (any participant killed, routed, or forcibly separated, or the target
  freed) fails the ritual — every participant spent that window fully
  committed and exposed for nothing.

**Turning to the Shadow** — permanently converting a captured channeler to
serve the Shadow.
- **Shadow-exclusive.** Requires **13 Black Ajah + 13 Myrddraal**, linked
  around a restrained, Shielded target — a house-rule extension of the
  Stilling/Gentling circle, doubled and mixed to reflect that this
  corrupts the person rather than just severing their ability.
- Same restrained-target and uninterrupted-window requirements as
  Stilling/Gentling, but the stakes are higher: failure isn't just a
  wasted attempt, it's a strategic catastrophe — 26 individual-scale
  Shadow units stationary and exposed in one place, all at once.
- A successfully turned channeler becomes a **controllable unit for the
  Shadow player.** This is the mechanical payoff behind unit conversion
  being Shadow-exclusive: alliances and turned allies, not gold or land,
  are the Shadow's core resource — see the Darkfriend Network in
  `08-economy-and-resources.md` and the updated Shadow brief in
  `05-factions.md`.

### Where Rituals happen: battle or stronghold
Per the earlier decision to support both:
- **Mid-battle (the risky gambit):** a full ritual circle can be assembled
  and attempted during a tactical battle, if the caster's side can hold
  position around a Shielded, captured target uninterrupted for the whole
  cast window. High risk (13 or 26 individual-scale units stationary and
  committed is an enormous target for the enemy to attack or interrupt),
  high reward (an instant, permanent result without waiting on the
  strategic layer).
- **Strategic layer (the safe path):** a captured channeler can instead be
  held as a **Prisoner** at a stronghold/province (a persistent unit
  status, not death — see `09-campaign-and-progression.md`), and the
  ritual run as a multi-turn strategic action once the required roster
  (13, or 13+13) is assembled there. Slower and safer — no battlefield
  interruption risk — but a held prisoner can potentially be rescued by
  the opposing side in the meantime, which is its own source of campaign
  drama.

### Capture as a battle outcome
Both paths above depend on **Capture** existing as a distinct battle
outcome from Kill: an order to subdue rather than destroy a Shielded or
broken (routing) enemy channeler, turning them into a Prisoner instead of
a casualty. See `04-tactical-battle-layer.md` for how this is expressed as
a battle order.

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
- Exact strength/skill threshold and contest formula for solo Shielding —
  Phase 6 balance pass, tracked alongside combat formulas in
  `04-tactical-battle-layer.md`.
- Exact Ritual cast-window length (mid-battle) and turn-count (strategic
  layer) — Phase 2/6 tuning.
- Whether and how mixed-affinity circles ever unlock (a relic, a campaign
  event, a tech-tree-style discovery) — flagged as a real design question,
  not yet recommended either way; fine to leave unbuilt for MVP since the
  single-affinity default fully supports both defined Rituals.
- Whether factions other than the Shadow ever get *any* form of forced
  conversion (even a weaker/costlier one) — current design keeps
  conversion Shadow-exclusive by decision; revisit only if playtesting
  shows other factions need an answer to it beyond Shielding/killing/
  ransoming captured channelers.
