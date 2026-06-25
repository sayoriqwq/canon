---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 canon wiki federation 中跨 sub-wiki 链接的语义。
type: concept
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Link Semantics

链接是 wiki federation 的结构语法，不是全部价值。

链接让 durable assertions 可追溯、可更新、可跨 sub-wiki 综合。链接不能让同一条 assertion 拥有多个真源。

## 链接类型

导航链接帮助 agent 和人找到页面。

Source 链接说明某个理论页面基于哪些 raw 或内部 source。

派生链接说明一个 sub-wiki 的 assertion 如何从另一个 sub-wiki 的 assertion 泛化而来。

对照链接说明两个相近概念或 claim 的边界。

维护链接说明变更一个页面时可能需要检查哪些相关页面。

## 约束

Cross-link 可以跨 sub-wiki。

Cross-link MUST NOT 复制被链接页面的 owning assertion。
