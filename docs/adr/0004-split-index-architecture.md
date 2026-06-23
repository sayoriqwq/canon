# ADR-0004: Split Index Architecture

## Status

Accepted

## Context

The user prefers single-responsibility documents and wants agents to learn the target structure from the beginning.

Keeping one large index while the repo is small would teach the wrong maintenance pattern.

## Decision

Use split index architecture from the start.

Each `index.md` owns only its next layer.

## Consequences

Even empty or small directories should have local indexes when they are part of the target structure.

Do not replace the layered index system with a single global catalog.
