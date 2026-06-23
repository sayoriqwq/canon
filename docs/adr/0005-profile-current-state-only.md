# ADR-0005: Profile Current State Only

## Status

Accepted

## Context

`profile/` is read by agents as current collaboration context. Old preferences can pollute agent behavior if preserved beside current preferences.

## Decision

`profile/` stores only current valid context.

Do not keep deprecated preferences, confidence values, or inferred/confirmed sections.

Use `updated` to help resolve conflicts.

## Consequences

When a preference changes, update or remove the old entry instead of preserving it in profile.

Historical audit belongs outside profile if it is ever needed.
