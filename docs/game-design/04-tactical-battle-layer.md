# Tactical Battle Layer

> Status: Draft — this is the project's signature system and its highest
> risk. Depends heavily on Q1–Q3 in `01-open-questions.md`. Everything
> below assumes the recommended answers there (turn-based/simultaneous,
> square grid, one-token-per-unit) unless noted.

## What problem this system solves

CoE5's battles resolve almost automatically — you commit an army and watch
the line grind. That's fine for a game about managing dozens of factions at
once, but it throws away exactly the thing Total War does best: a battle
that rewards understanding terrain, positioning, and timing. This layer
exists to bring that back, without inheriting Total War's cost (full 3D
armies, physics, pathfinding at the level of individual soldiers).

## The battlefield

- A **grid** (square, per Q2), taller than it is wide — recommended around
  9–13 columns by 14–20 rows (see Q3).
- **Terrain occupies grid cells** and is drawn from the province the battle
  is fought in (a forest province starts a battle with forest cells; a
  river-crossing province starts with a river bisecting the field and a
  limited number of fordable/bridged cells).
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

The player's forces deploy in the **south** rows of the grid; the enemy
deploys in the **north** rows. This is a deliberate departure from the
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

## Deployment phase

Before the battle starts, the player is given a **deployment zone**
(typically the southern 2–4 rows, terrain-dependent) and places units
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

Recommended model (per Q1): **turn-based with simultaneous resolution.**

Each battle round:

1. **Order phase.** The player selects units (individually or as a group)
   and assigns orders: move to a cell, hold position, attack a target,
   use a weave/ability, change formation, retreat. The player can freely
   inspect the whole field, undo orders, and take as long as they want —
   there's no clock. The AI plans its round at the same time, invisibly.
2. **Resolution phase.** Both sides' orders execute together. Movement,
   attacks, and ability effects resolve according to fixed, transparent
   rules (see "Resolution order" below) so the outcome is a
   deterministic consequence of the orders given, not a hidden dice roll
   the player couldn't have anticipated.
3. Repeat until one side breaks (see Morale) or is destroyed, or a
   round/turn limit forces a result.

This gives the "actively micro units to win" feeling the user wants — the
player is constantly making and revising decisions as the fight develops —
without needing real-time reflexes or real-time engineering complexity.

### Resolution order (first pass, to be validated in Phase 2 prototyping)

1. Weaves/abilities with a "cast" step that can be interrupted resolve
   first, in priority order.
2. Movement resolves (simultaneous moves into the same cell are blocked/
   contested per a defined tie-break rule).
3. Melee and ranged attacks resolve based on final positions.
4. Morale checks resolve last, based on the round's losses.

### Formations and facing

Units have a **facing** and can be caught **flanked or from behind**, which
matters for damage and morale — this is the primary way "positioning" pays
off mechanically, and it's what makes the deployment phase and the terrain
matter rather than being set dressing. Grouped units can move as a
formation (keep relative positions) or be ordered individually.

### Morale and routing

Units track morale separately from health. Taking losses, being flanked,
losing a commander, or facing units/effects specifically designed to break
morale (Myrddraal presence, certain weaves) degrades it. A broken unit
routs — flees toward its own board edge and stops following orders — rather
than fighting to the last soldier. This keeps battles from being pure
attrition math and gives "make the enemy break" its own tactical texture
distinct from "kill everything."

### Channeling in battle

Channelers are the highest-impact, highest-risk units on the field:

- Weaves used in battle cost the channeler's Power reserve for that battle
  and carry the taint/burnout risk described in
  `06-magic-and-channeling.md` — a channeler who overreaches in one battle
  pays for it afterward, sometimes permanently.
- Some weaves have a visible "tell" (a cast step other side can see and
  potentially interrupt or flee from), which is what keeps a channeler from
  being a simple win-button — positioning to protect or to kill an enemy
  channeler becomes a real tactical thread.

## Victory conditions (per battle)

Default: a side wins when the enemy force is destroyed, has entirely
routed off the field, or fully retreats. Some battles (sieges, rearguard
actions) may use objective-based conditions (hold a cell for N rounds,
break through to the enemy's board edge) — flagged here as a Phase 5
content concern, not an MVP requirement.

## What this deliberately does not do

- No unit-level pathfinding around individual obstacles mid-cell — movement
  is cell-to-cell on the grid, not physics-simulated.
- No hidden non-determinism in combat resolution that the player couldn't
  have reasoned about from the order phase (no "surprise, that attack just
  missed for no visible reason" — see `04` resolution order above).
- No requirement for split-second reaction time — the order phase has no
  clock.

## Open items

- Exact formula for combat resolution (to-hit, damage, terrain modifier
  stacking) — belongs in a balance-focused follow-up once the shape above
  is validated in a Phase 2 prototype.
- Whether group orders support waypoints/multi-step move orders, or only
  single-destination-per-round — recommend starting with single-destination
  and adding waypoints only if playtesting shows it's needed.
- Siege-specific rules (walls as a battle-wide feature rather than a single
  terrain cell) — Phase 5 content concern.
