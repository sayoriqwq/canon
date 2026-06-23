---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 canon 从一开始使用拆分 index 架构的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0004: 拆分式 Index 架构

## 背景

用户偏好单一职责文档，并希望 agent 从一开始学习目标结构。

因为仓库还小就保留一个大 index，会训练出错误的维护模式。

## 决策

从一开始使用 split index architecture。

每个 `index.md` 只负责下一层。

## 后果

如果某个目录属于目标结构，即使暂时为空或很小，也 SHOULD 有本地 index。

MUST NOT 用单一全局目录替代分层 index system。
