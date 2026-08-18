# Architecture / Design Decision Records

This folder holds short records of decisions that were non-obvious enough
to be worth explaining to a future reader — the "why," not the "what" (the
docs in `docs/game-design/` and `docs/technical-design/` already cover the
what, and are the ones that should be kept current; ADRs are a permanent,
dated log and are **not** edited after the fact).

## When to write one

Write an ADR when a decision:
- Overrides or narrows something a design/technical doc would otherwise
  suggest
- Was genuinely contested (more than one reasonable option existed) and
  the reasoning for picking one is worth preserving
- Resolves an entry from `docs/game-design/01-open-questions.md` or
  similar in a technical-design doc — the ADR is where the *why* lives;
  the open-questions doc's "Resolved" section just links to it

Don't write one for routine content additions (a new unit doesn't need an
ADR) or for anything already fully explained by the doc it lives in.

## Format

Use the standard lightweight ADR shape (Michael Nygard's template):

```
# NNNN. Short title of the decision

Date: YYYY-MM-DD
Status: Proposed | Accepted | Superseded by NNNN

## Context
What's the situation that forces a decision?

## Decision
What did we decide?

## Consequences
What does this make easier or harder going forward?
```

Number sequentially (`0001-...`, `0002-...`), never reuse or renumber.
A superseded ADR stays in place with its status updated — it's history,
not a mistake to erase.

See `0001-record-architecture-decisions.md` for the first (self-referential)
example.
