---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 agent-facing 文档应优先使用模式而非仅靠描述的判断。
type: claim
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Agent-facing Docs Need Patterns, Not Descriptions Alone

## 判断

面向 agent 的规范不能只依赖描述性散文；它们应优先提供可识别、可复用、可检查的 [agent-facing pattern](../concepts/agent-facing-pattern.md)。

描述可以解释意图，但模式决定 agent 实际可执行的边界。

## 支持

稳定字段、枚举值、固定章节、frontmatter 和检查清单都能减少模型猜测。只写“保持清晰”或“注意结构”会把执行边界交给模型自由补全。

## 连接

- [Frontmatter for Persistent State](../patterns/frontmatter-for-persistent-state.md)
- [Normative Keyword Ladder](../patterns/normative-keyword-ladder.md)
- [Assertion-level Review](../patterns/assertion-level-review.md)
