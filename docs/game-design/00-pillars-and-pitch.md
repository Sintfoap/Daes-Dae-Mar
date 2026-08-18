# Pillars & Pitch

> Status: Draft — foundational, should change rarely and only deliberately.

## Elevator pitch

Play as one faction in a Wheel of Time world where every other major power —
the White Tower, the Black Tower, the Seanchan, the Shadow, the Borderlands —
is simultaneously playing its own game for the same stakes. Manage your
faction on a strategic map, the way you would in Conquest of Elysium: simple,
iconic, and full of asymmetric factions with almost nothing in common with
each other. When armies meet, the game drops into a tactical battle on a
terrain-covered grid, your forces entering from the south and theirs from the
north, and you fight it out not by picking "attack" and watching, but by
laying out your formation and then actively directing units as the fight
unfolds.

## Why these two games, specifically

| | Conquest of Elysium 5 | Total War | Daes Dae Mar |
|---|---|---|---|
| Visual approach | Simple 2D icons/portraits, no unit models | High-fidelity 3D armies | 2D icons/portraits, CoE-simple |
| Strategic layer | Many wildly asymmetric AI factions, all acting with agency | Faction management, but each faction plays similarly | Many asymmetric factions (WoT powers), CoE-style |
| Battle resolution | Two lines meet and grind — minimal tactical input | Full battlefield freedom: flanking, terrain, formations | Grid-based freedom: terrain, positioning, flanking — but still a grid |
| Battle input model | Mostly automatic once armies meet | Real-time (or turn-based in some titles) direct unit control | Deploy, then actively issue orders as the fight plays out |
| Orientation | Left-to-right line clash | Free 3D orientation | Bottom-to-top: your line advances north into theirs |
| Scope philosophy | Breadth over fidelity — many factions, low art cost per unit | Fidelity over breadth — fewer factions, high art cost per unit | Breadth over fidelity, matching CoE — this is what makes a large WoT faction roster affordable |

The reason to take CoE5's simplicity isn't just budget — it's that the
Wheel of Time cast of factions is genuinely huge (Aes Sedai, Asha'man,
Seanchan, Aiel, half a dozen Borderland and southern nations, Shadowspawn,
the Sea Folk, the Ogier...). A high-fidelity Total War approach can afford
maybe half a dozen well-realized factions. A CoE5-style approach can afford
most of the setting, which is the more interesting game for this IP.

The reason to add battlefield freedom on top of CoE5's model is that a WoT
battle *should* feel different depending on who's fighting: Aiel ambushing
from broken ground, Seanchan damane raking a battle line with fire from the
back ranks, Trollocs breaking on a Whitecloak shield wall at a river
crossing. A pure line-clash can't express any of that. It doesn't need full
3D freedom to do it — a grid with real terrain and live orders is enough.

## The four pillars

Every design decision should be checked against these. If a proposed feature
doesn't clearly serve one of them, it's probably scope creep.

### 1. Visual simplicity as a scope strategy, not a limitation
Icon/portrait-based units, minimal animation, CoE5-grade production values.
This isn't "we'll upgrade the art later" — it's a permanent decision that
lets a small team field a large, varied roster. Depth lives in systems and
writing, not in rendering.

### 2. A strategic layer where every faction is a real player
Not "the player's empire vs. generic AI opposition." Every major WoT power
on the map is pursuing its own goals with its own asymmetric toolkit, the
way CoE5's cults and nations do. The Whitecloaks aren't a reskinned generic
faction with a different color — they play by different rules (no
channelers, ever; different resource priorities; different win conditions
in the fiction).

### 3. A grid battlefield with room to maneuver
Terrain that matters (hills, forests, river crossings, fortifications),
armies that enter from opposite ends of a vertical field, a deployment
phase where the player chooses formation and positioning, and a battle phase
where the player can pause and give orders to individual units or groups as
the fight develops — not just "commit and watch." This is Total War's
contribution to the hybrid, expressed on a grid instead of open 3D terrain.

### 4. The One Power is the core power-fantasy *and* the core risk
Channeling should be the single most powerful tool in the game at both
layers — and the single riskiest. Saidin's taint, saidar's burnout risk,
gentling/stilling, Compulsion, balefire — these aren't flavor text, they're
mechanics with real strategic and tactical weight. A faction built around
channelers should feel meaningfully different to play than one without.

## Explicit non-goals

Stated up front so scope discussions have a fast "no" available:

- **Not open 3D terrain.** The battlefield is a grid. Freedom comes from
  terrain variety and order-giving, not from free-form movement or physics.
- **Not real-time-only with no pause.** Whatever the final pacing model
  (see open questions), the player must be able to make deliberate,
  unhurried tactical decisions — this is a thinking-person's battle, not a
  reflex test.
- **Not a 1:1 historical-battle simulator.** Unit counts and battle scale
  are abstracted (squads/companies represented by tokens, CoE5-style), not
  individually simulated soldiers.
- **Not an MMO or persistent multiplayer world**, at least not for an
  initial release. Multiplayer may be worth revisiting later, but nothing
  in Phase 1–3 should assume it.
- **Not a retelling of the books' plot.** The setting, powers, and factions
  are the *Wheel of Time* as of a chosen point in its history (see open
  questions), used as a sandbox — not a scripted adaptation of the novels'
  events.
