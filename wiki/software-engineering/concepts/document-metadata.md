---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 document metadata 作为文档级持久状态。
type: concept
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Document Metadata

## 定义

Document metadata 是文档级别的持久状态信息，通常放在 Markdown frontmatter 中。

它描述读者、生成来源、review 状态、用途和更新时间等稳定信息。正文中需要展开的概念、理由和规则不应塞进 metadata。

## 关系

[Document Module](document-module.md) 需要 metadata 提供机器可读入口。

[Frontmatter for Persistent State](../patterns/frontmatter-for-persistent-state.md) 是 document metadata 的主要实践模式。
