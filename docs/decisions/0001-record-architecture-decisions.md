# 0001. Record architecture and design decisions as ADRs

Date: 2026-08-18
Status: Accepted

## Context

This project is explicitly meant to be "robust and easy to add to from a
human perspective," per the founding brief in the root README. Design and
technical docs (`docs/game-design/`, `docs/technical-design/`) describe the
current, intended state of the system well, but they don't naturally
preserve *why* a contested decision went one way instead of another —
updating a doc in place tends to overwrite that context.

## Decision

Non-obvious or contested decisions get a short, dated, immutable record in
`docs/decisions/`, following the format in `docs/decisions/README.md`.
Design/technical docs stay current and get edited freely; ADRs are a
historical log and don't get rewritten after acceptance (only superseded by
a new one).

## Consequences

Future contributors (including future sessions working on this project)
can find out why something is the way it is without archaeology through
commit history. The cost is small discipline overhead: contested decisions
need a few extra minutes to write up. Worth it for a project explicitly
optimizing for long-term extensibility.
