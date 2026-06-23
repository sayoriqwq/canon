# ADR-0002: Four Peer Systems

## Status

Accepted

## Context

Canon needs to handle unresolved fragments, preserved source material, digested theory, and current user context without mixing their lifecycles.

## Decision

Canon has four peer systems:

- `fragments/`: authoritative fragment judgment.
- `raw/`: preserved source material.
- `wiki/`: digested theory assets.
- `profile/`: current user and collaboration model.

## Consequences

Each system has its own index and maintenance rules. Do not collapse these layers into one notes directory.
