# Tactical Battle Layer

> Status: Draft — core decisions locked (real-time-with-pause pacing, hex
> grid; see `docs/decisions/0002-real-time-with-pause-battle-pacing.md`
> and `docs/decisions/0003-hex-grid.md`). Remaining detail (exact
> battlefield size, resolution formulas) is still open and belongs to
> Phase 2 prototyping.

## What problem this system solves

CoE5's battles resolve almost automatically — you commit an army and watch
the line grind. That's fine for a game about managing dozens of factions at
once, but it throws away exactly the thing Total War does best: a battle
that rewards understanding terrain, positioning, and timing. This layer
exists to bring that back, without inheriting Total War's cost (full 3D
armies, physics, pathfinding at the level of individual soldiers).

## The battlefield

- A **hex grid** (`docs/decisions/0003-hex-grid.md`), taller than it is
  wide — roughly 9–13 hexes wide by 14–20 deep as a starting point (see
  `docs/game-design/01-open-questions.md` Q3 for the still-open exact
  sizing).
- **Terrain occupies hexes** and is drawn from the province the battle is
  fought in (a forest province starts a battle with forest hexes; a
  river-crossing province starts with a river bisecting the field and a
  limited number of fordable/bridged hexes).
- Terrain types and their effects (first pass — to be tuned in
  playtesting):
  | Terrain | Effect |
  |---|---|
  | Open ground | No modifier — baseline |
  | Hill | Defense bonus; ranged units gain range/accuracy; blocks line of sight for units below it |
  | Forest | Movement penalty; ranged accuracy penalty against units inside it; ambush-friendly (Aiel relevant) |
  | River / water | Impassable except at fords/bridges; crossing units are vulnerable mid-cross |
  | Fortification / wall | Hard to cross without siege capability; strong defense bonus to units behind it |
  | Road | Movement bonus |

## Orientation: driven by the strategic attack, not a fixed axis

**Decision (`docs/decisions/0006-strategic-driven-entry-and-deployment.md`):**
there is no fixed "player enters south, enemy enters north." Instead, the
edge an army enters the battlefield from is determined by **where it
attacked from on the strategic map.** Attacking a province from its
western neighbor lands your army on the battlefield's west edge; attacking
from the north lands you on the north edge; and so on. The defender isn't
pinned to a fixed opposite edge — see Deployment below — but the
attacker's entry edge is always a direct read of the actual geography of
the campaign move that triggered the battle.

This requires the strategic layer to know, for any two adjacent provinces,
which direction one lies in relative to the other (see
`03-strategic-layer.md`), and the tactical layer to orient the hex
battlefield so that direction maps onto one of the hex grid's six edges.

Why this instead of a fixed axis:
- It makes the tactical battle a direct continuation of the strategic
  decision that caused it — attacking from the Blight-adjacent province
  puts Shadowspawn on the northern tree line for real, not just in flavor
  text.
- It gives terrain and deployment (below) something real to respond to:
  defending the same province against an attack from the river crossing
  in the east is a different battle than defending it against an attack
  out of the southern hills, using the same battlefield.
- It leaves room — without needing a redesign later — for more than one
  attacking force to converge on the same province from different
  directions in the same turn, each entering from its own edge with the
  defender caught between them. Full multi-edge battles are a Phase 5+
  enhancement (see Open items), not an MVP requirement, but the entry-edge
  model supports it naturally when it's built.
- Most individual battles will still read as "one side pushing toward the
  other," the same way the original fixed framing intended — the
  difference is that which edge is "forward" now depends on the actual
  campaign, not a fixed screen direction. The presentation layer should
  orient the camera/UI to match the strategic bearing the player is used
  to (see the sim-vs-render orientation note in
  `docs/technical-design/04-battle-simulation-design.md`), so "I'm
  attacking from the west" feels consistent between the strategic map and
  the battle.

## Deployment phase: bounded, and asymmetric between attacker and defender

Deployment freedom is real on both sides, but it isn't symmetric — the
attacker is just arriving at the province's edge; the defender is fighting
on ground they already hold.

- **Attacker deployment zone:** a band of hexes adjacent to the attacker's
  entry edge (the "beachhead"). The attacker chooses how to arrange units
  within that band — concentrated for a strong initial push, or spread to
  cover more of the edge — but can't deploy deep into the province before
  the battle starts.
- **Defender deployment zone:** the rest of the battlefield, minus a
  buffer near the attacker's entry edge reserved for their arrival. This
  is deliberately much more generous than the attacker's — the defender
  can make a stand forward at a chokepoint, fall back to a fortification,
  spread thin to cover multiple approach lanes, or hold a reserve deep in
  the province, all before a single order is given.
- Both zones are still bounded, not the whole map — this keeps the
  deployment phase fast to read and keeps the entry-edge model meaningful
  (an attacker who could deploy anywhere would make "where you attacked
  from" cosmetic).

The enemy AI deploys under the same rules and the same terrain, which is
what makes the strategic-layer decision to attack from one direction
rather than another a real tactical choice, not flavor.

### Terrain-linked deployment trade-offs

This is where deployment stops being just "arrange units" and starts being
a real strategic choice with matched upside and downside, using the same
terrain from `The battlefield` above:

| Deployment choice | Upside | Downside |
|---|---|---|
| Hold a **hill** in your zone | Defense/ranged bonus | Farther to retreat if routed — routing units are exposed longer |
| Deploy inside a **forest** | Concealment/ambush bonus (may go unspotted until the enemy is adjacent) | Slower to reposition afterward; weaker formation bonuses |
| Concentrate at a **chokepoint** (ford, pass, gate) | A small force can hold a much larger one | A single flank collapse — or a channeler weave that clears the chokepoint — is proportionally catastrophic; contests no other ground |
| **Spread across multiple lanes** | Harder to outflank entirely; better map control | Each concentration is individually weaker; reinforcing between them costs real time on the clock (this is a real-time battle — see `docs/decisions/0002` — so repositioning has a literal time cost) |
| Deploy behind a **fortification** (province-dependent) | Strong defense bonus | Cedes the open field; the attacker may bypass and pressure elsewhere instead of attacking the fortified point directly |
| Hold a **reserve** off the front line | Full flexibility to reinforce wherever the fight goes badly | Outnumbered in the opening exchanges |

These trade-offs should live as **terrain and unit tags in data**
(`docs/technical-design/02-data-driven-content.md`) — e.g., `hill` carries
`defense_bonus` and `rout_distance_penalty`; a unit with an `ambush` tag
draws its concealment specifically from `forest` terrain. Deployment
strategy should be an emergent property of terrain + unit data, not a
separate hardcoded system, so a new terrain type or unit automatically
slots into the same trade-off space.

## Battle phase: order-giving

**Model (per `docs/decisions/0002-real-time-with-pause-battle-pacing.md`):
real-time with pause**, matching Total War's own order-giving directly.

- The battle runs on a continuous clock. The player can **pause at any
  time** — freely, with no limit — to survey the whole field and issue or
  revise orders, then unpause to watch them play out.
- Orders: move to a hex (or along a path of hexes), hold position, attack a
  target, use a weave/ability, change formation, retreat. Orders can be
  given to individual units or to a selected group, and can be queued or
  changed at any pause.
- The AI plans and issues its own orders continuously in the background,
  using the same order types and the same information the player would
  have (no orders the player couldn't also give).
- Movement, attacks, weave casting, and morale checks all happen
  continuously while unpaused rather than resolving in discrete rounds —
  see `docs/technical-design/04-battle-simulation-design.md` for how this
  is kept deterministic under the hood (a fixed-timestep simulation clock
  that the pause/unpause and player orders are timestamped against, not
  wall-clock time).

This is what gives the "actively micro units to win" feel the project is
built around: the player is constantly watching the field develop and
reacting, exactly as in Total War, just expressed on a hex grid instead of
open 3D terrain. The unlimited pause is what keeps this from requiring
reflexes — a player who wants to treat every moment as a puzzle they can
freeze and study is fully supported; a player who wants to play it more
continuously can do that too.

### Formations and facing

Units have a **facing** and can be caught **flanked or from behind**, which
matters for damage and morale — this is the primary way "positioning" pays
off mechanically, and it's what makes the deployment phase and the terrain
matter rather than being set dressing. The hex grid's 6-directional
adjacency gives flanking a cleaner geometric basis than a square grid would
have (no ambiguous diagonal cases). Grouped units can move as a formation
(keep relative positions) or be ordered individually.

### Morale and routing

Units track morale separately from health. Taking losses, being flanked,
losing a commander, or facing units/effects specifically designed to break
morale (Myrddraal presence, certain weaves) degrades it continuously as the
fight plays out. A broken unit routs — flees toward its own board edge and
stops following orders — rather than fighting to the last soldier. This
keeps battles from being pure attrition math and gives "make the enemy
break" its own tactical texture distinct from "kill everything."

### Channeling in battle

Channelers are the highest-impact, highest-risk units on the field:

- Weaves used in battle cost the channeler's Power reserve for that battle
  and carry the taint/burnout risk described in
  `06-magic-and-channeling.md` — a channeler who overreaches in one battle
  pays for it afterward, sometimes permanently.
- Casting a weave has a visible **cast-time window** on the clock —
  telegraphed and interruptible in real time (the enemy can see it coming
  and has a window to close distance, retreat, or focus the channeler down
  before the weave completes) — which is what keeps a channeler from being
  a simple win-button. Positioning to protect or to kill an enemy channeler
  becomes a real tactical thread, now expressed as a race against a visible
  timer rather than a round-based interrupt.

## Victory conditions (per battle)

Default: a side wins when the enemy force is destroyed, has entirely
routed off the field, or fully retreats. Some battles (sieges, rearguard
actions) may use objective-based conditions (hold a hex for a duration,
break through to the enemy's board edge) — flagged here as a Phase 5
content concern, not an MVP requirement.

## What this deliberately does not do

- No unit-level pathfinding around individual obstacles mid-hex — movement
  is hex-to-hex on the grid, not physics-simulated.
- No hidden non-determinism in combat resolution that the player couldn't
  have reasoned about — the underlying fixed-timestep simulation is
  deterministic even though it's presented as free-flowing real time (see
  `docs/technical-design/04-battle-simulation-design.md`).
- No requirement to react instantly — pausing is unlimited and free, so no
  decision is ever forced under a reflex clock even though the game runs
  in real time when unpaused.

## Open items

- Exact battlefield size in hexes, and exact deployment zone depth for
  both attacker and defender — Q3 in `01-open-questions.md`, still open.
- Exact formula for combat resolution (to-hit, damage, terrain modifier
  stacking, attack cooldown/rate) — belongs in a balance-focused follow-up
  once the shape above is validated in a Phase 2 prototype.
- Whether group orders support waypoints/multi-step move paths, or only a
  single destination per order — recommend starting with waypoint support
  from the outset, since real-time movement (unlike round-based movement)
  makes multi-leg paths a natural and low-cost thing to support; revisit if
  Phase 2 prototyping finds otherwise.
- Siege-specific rules (walls as a battle-wide feature rather than a single
  terrain hex) — Phase 5 content concern.
- Full multi-edge/multi-front battles (more than one attacking force
  entering from different edges in the same battle) — Phase 5+
  enhancement; MVP handles one attacker edge and one defender per battle.
- What happens when neither side is cleanly "the attacker" (e.g., two
  armies both moved into a contested/neutral province the same turn) —
  likely resolved by giving each force its own entry edge based on its own
  origin province, even when those edges aren't opposite each other,
  which is a reasonable fallback but hasn't been fully specced.
