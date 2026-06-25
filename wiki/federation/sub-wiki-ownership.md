---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 sub-wiki 的拆分边界和 ownership 判断方式。
type: concept
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Sub-wiki Ownership

Sub-wiki 是 assertion ownership 区域，不是主题文件夹。

一个页面属于哪个 sub-wiki，取决于它主张的 durable assertion 类型，而不是它提到了哪些主题。

## 判断标准

问“这条 assertion 在维护谁的当前状态或理论？”

- 维护 sayori 当前模型、偏好、协作语义：`wiki/profile/`。
- 维护共享词义、关系语义、边界：`wiki/vocabulary/`。
- 维护 canon wiki federation 理论：`wiki/federation/`。
- 维护软件工程和 agent-facing 文档理论：`wiki/software-engineering/`。

## 例子

“sayori 偏好 assertion-level review”属于 `wiki/profile/`。

“assertion-level review 是一种可复用文档维护模式”属于 `wiki/software-engineering/`。

“assertion 这个词在 canon 中的定义”属于 `wiki/vocabulary/`。

“profile 和 software-engineering 如何跨链”属于 `wiki/federation/`。
