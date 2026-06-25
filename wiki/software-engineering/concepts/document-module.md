---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 Markdown 文档作为可组合模块的概念。
type: concept
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Document Module

## 定义

Document module 是把一份 Markdown 文档视为可索引、可链接、可组合、可复用的模块单元。

它反对把文档当作散乱文本容器。文档需要稳定边界、明确职责和可维护结构，才能在长期协作中被人和 agent 可靠使用。

## 关系

Document module 由 [document metadata](document-metadata.md)、[assertion](assertion.md) 和结构化正文共同构成。

它支持 [Split Index Document Architecture](../patterns/split-index-document-architecture.md)，并受到 [Document structure trains maintenance](../claims/document-structure-trains-maintenance.md) 的约束。
