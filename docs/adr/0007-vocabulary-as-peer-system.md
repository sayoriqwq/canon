---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 vocabulary 作为第五个并列系统的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0007: Vocabulary 作为并列系统

## 背景

Canon 最初把核心术语放在 `CONTEXT.md` 的 `Vocabulary` 小节中。随着 `profile/` 开始保存跨目录偏好，词汇表也需要覆盖 canon、agent、profile 等不同语义层级；继续把所有词塞进 `CONTEXT.md` 会让它承担过多职责。

## 决策

建立 `vocabulary/` 作为和 `fragments/`、`raw/`、`wiki/`、`profile/` 并列的第五个系统。`CONTEXT.md` 只路由到 `vocabulary/`，不保留小型核心词汇副本；完整术语按层级拆到 `vocabulary/` 下。

## 后果

新增或修改跨目录术语时，优先更新 `vocabulary/`。`CONTEXT.md` 不再是词汇表，也不保留核心术语副本。
