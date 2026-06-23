---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 ADR 只服务 canon 仓库反馈的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0006: ADR 只服务 Canon Feedback

## 背景

Canon 包含理论 wiki，但 repository architecture decisions 不会自动成为软件工程理论。

混合仓库 feedback 和 theory 会污染 wiki。

## 决策

`docs/adr/` 只记录本仓库结构和维护行为相关的决策。

## 后果

MUST NOT 把 canon architecture decisions 提升进 `wiki/`，除非用户明确要求把它们泛化成软件工程理论。
