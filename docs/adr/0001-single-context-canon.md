---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 canon 作为 single-context 仓库的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0001: 单一上下文 Canon

## 背景

Canon 有多个层：`fragments/`、`raw/`、`wiki/`、`profile/` 和 `vocabulary/`。这些层容易被误认为彼此独立的 context。

本仓库的真实目的统一：服务一个用户的长期软件工程理论建设。

## 决策

Canon 是 single-context 仓库。MUST NOT 创建 `CONTEXT-MAP.md`。

共享意义放在根 `CONTEXT.md`，导航使用分层 `index.md`。

## 后果

Agent SHOULD 把 `fragments/`、`raw/`、`wiki/`、`profile/`、`vocabulary/` 视为同一系统的不同层，而不是独立 domain。

如果 canon 以后包含多个相互独立的理论系统，再回头审查这个决策。
