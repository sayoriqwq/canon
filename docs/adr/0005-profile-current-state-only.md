---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 profile 只保存当前可迁移用户上下文的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0005: Profile 只保存当前可迁移用户上下文

## 背景

Agent 会把 `profile/` 当作当前协作上下文读取。如果旧偏好和当前偏好一起保留，会污染 agent 行为。

Canon 也有 repository-specific 操作规则。如果这些规则进入 `profile/`，agent 可能会把 canon-only 的行为错误应用到无关目录。

## 决策

`profile/` 只保存当前有效、且跨目录仍然成立的用户上下文和偏好。

MUST NOT 保留 deprecated 偏好、confidence 字段，或 inferred/confirmed 分区。

MUST NOT 把 canon-specific 结构、工作流或目录规则放进 `profile/`；这些内容 SHOULD 放在 `HARNESS.md` 或 ADR 中。

使用 `updated` 辅助解决冲突。

## 后果

偏好变化时，直接更新或删除旧条目，不在 profile 中保留旧版本。

如果未来需要历史审计，它应存在于 profile 之外。

仓库操作规则留在 `HARNESS.md`。
