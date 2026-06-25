---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义面向 agent 的稳定输入输出模式。
type: concept
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Agent-facing Pattern

## 定义

Agent-facing pattern 是面向 agent 的稳定输入或输出结构，例如固定字段、枚举值、目录命名、章节标题、状态流转格式或检查清单格式。

它的作用是减少 agent 对上下文的猜测，让文档可以被读取、生成、检查和继续处理。

## 关系

Agent-facing pattern 支持 [Agent-facing docs need patterns, not descriptions alone](../claims/agent-docs-need-patterns-not-descriptions.md)。

[Frontmatter for Persistent State](../patterns/frontmatter-for-persistent-state.md) 和 [Normative Keyword Ladder](../patterns/normative-keyword-ladder.md) 都是 agent-facing pattern。
