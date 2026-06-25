---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 描述用 frontmatter 保存文档级持久状态的模式。
type: pattern
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Frontmatter for Persistent State

## 模式

把文档级持久状态放入 frontmatter，把正文论述保留在结构化正文中。

Frontmatter 适合保存 `audience`、`authors`、`reviewed_by`、`purpose`、`updated` 等稳定状态。概念展开、理由、规则和争议不应塞进 metadata。

## 适用场景

- 文档需要被 agent 稳定读取。
- 文档状态需要跨会话保留。
- 后续工具或脚本需要检查文档结构。

## 连接

- [Document Metadata](../concepts/document-metadata.md)
- [Agent-facing docs need patterns, not descriptions alone](../claims/agent-docs-need-patterns-not-descriptions.md)
