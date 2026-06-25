---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 canon wiki federation 中唯一真源和 assertion ownership 的规则。
type: claim
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Source of Truth

每条 durable assertion 只能有一个 source of truth。

在 canon 中，source of truth 可以是 raw source，也可以是一个 owning sub-wiki 页面。其它位置只能链接、引用、摘要、派生、泛化或投影。

## 规则

Profile assertion 的真源在 `wiki/profile/`。

Vocabulary assertion 的真源在 `wiki/vocabulary/`。

Federation architecture theory 的真源在 `wiki/federation/`。

Software engineering theory 的真源在 `wiki/software-engineering/`。

Raw 原文的真源在 `raw/` 或 upstream。Wiki 页面可以消化 raw，但不能替代 raw。

## 反模式

同一条偏好同时写在 `wiki/profile/` 和 `wiki/software-engineering/` 是重复真源。

正确做法是：`wiki/profile/` 保存当前偏好；`wiki/software-engineering/` 保存从该偏好泛化出的理论 assertion，并链接回 source note 或 profile 页面。
