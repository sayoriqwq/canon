# ADR-0001: Single Context Canon

## Status

Accepted

## Context

Canon has multiple layers: `fragments/`, `raw/`, `wiki/`, and `profile/`. These layers could be mistaken for separate contexts.

The repository's actual purpose is unified: support long-term software engineering theory building for one user.

## Decision

Canon is a single-context repository. Do not create `CONTEXT-MAP.md`.

Use root `CONTEXT.md` for shared meaning and use layered `index.md` files for navigation.

## Consequences

Agents should treat `fragments/`, `raw/`, `wiki/`, and `profile/` as layers of one system, not separate domains.

If canon later contains multiple independent theory systems, revisit this decision.
