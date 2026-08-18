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

## Orientation: bottom-to-top, not left-to-right

The player's forces deploy in the **south** hexes of the grid; the enemy
deploys in the **north** hexes. This is a deliberate departure from the
traditional left-right clash for a few concrete reasons:

- It reads naturally as "pushing into enemy territory," which matches the
  strategic layer (you're advancing on a province, not sliding sideways
  past it).
- UI real estate splits cleanly: player unit info/portraits anchor to the
  bottom of the screen near the player's own army, enemy info anchors to
  the top — no need to mirror UI elements left/right.
- It reinforces that this is a grid tactics game, not a simulated
  battlefield viewed from the side — the top-down framing is honest about
  what the system actually is.

The hex grid decision doesn't change this framing — a hex grid still has a
clear south edge and north edge, just with 6-directional adjacency instead
of 4/8.

## Deployment phase

Before the battle starts, the player is given a **deployment zone**
(typically the southern 2–4 hex rows, terrain-dependent) and places units
within it freely: front line, flanks refused or extended, ranged units
held back, a channeler tucked behind infantry, cavalry held on a flank to
exploit open ground. This is where CoE5's "just commit the stack" gives way
to real Total-War-style pre-battle planning — but bounded to a grid, so it
stays fast to resolve and easy to read.

The enemy AI deploys with the same freedom, using the same terrain, which
is what makes terrain choices during the strategic layer's battles matter
(attacking into a forested province against Aiel is a different tactical
problem than attacking across open plains).

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

- Exact battlefield size in hexes, and exact deployment zone depth — Q3 in
  `01-open-questions.md`, still open.
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
