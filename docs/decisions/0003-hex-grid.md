# 0003. Hex grid over square grid

Date: 2026-08-18
Status: Accepted

## Context

`docs/game-design/01-open-questions.md` Q2 needed a resolved battlefield
geometry. The drafted recommendation was a square grid, on the reasoning
that it reads closer to CoE5's visual simplicity and pairs more naturally
with rectangular terrain features (rivers, walls, forest blocks). Hex grids
offer better flanking/movement feel at the cost of extra tooling
complexity.

## Decision

The tactical battlefield uses a hex grid.

## Consequences

- Flanking, terrain adjacency, and movement should read more naturally
  than on a square grid — no diagonal-distance ambiguity, and 6-directional
  facing gives flanking bonuses (`docs/game-design/04-tactical-battle-layer.md`)
  a cleaner geometric basis.
- Terrain features that are naturally rectangular in the fiction (river
  crossings, wall lines) need to be authored as runs of hexes rather than
  grid rows/columns — a minor authoring consideration for whoever lays out
  province terrain, not a blocker.
- Coordinates move from row/column to axial or cube hex coordinates
  throughout the simulation and any content that references battlefield
  position — `docs/technical-design/04-battle-simulation-design.md` was
  updated accordingly.
- Pathfinding and adjacency logic need hex-aware implementations (6
  neighbors instead of 4/8) — a known, well-documented problem space, not a
  novel one, but real implementation work that a square grid would have
  avoided.
- Battlefield orientation was later decoupled from a fixed axis entirely
  (see `0006-strategic-driven-entry-and-deployment.md`) — a hex grid
  supports an entry edge on any of its six sides equally well, so that
  change didn't require revisiting this one.
