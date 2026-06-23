# ADR-0006: ADRs Serve Canon Feedback Only

## Status

Accepted

## Context

Canon contains a theory wiki, but repository architecture decisions are not automatically software engineering theory.

Mixing repository feedback with theory would pollute the wiki.

## Decision

`docs/adr/` records decisions about this repository's structure and maintenance behavior only.

## Consequences

Do not promote canon architecture decisions into `wiki/` unless the user explicitly asks to generalize them into software engineering theory.
