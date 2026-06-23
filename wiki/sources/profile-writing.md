---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 消化 profile/writing 中的写作偏好，并连接到 wiki 理论资产。
type: source
status: active
confidence: high
sources: []
raw:
  - ../../profile/writing/concept.md
  - ../../profile/writing/assertions.md
  - ../../profile/writing/io-patterns.md
  - ../../profile/writing/normative-keywords.md
  - ../../profile/writing/language.md
updated: 2026-06-24
---

# Profile Writing Source Note

## Source 边界

本页把 `profile/writing/` 作为内部 source 消化。`profile/writing/` 仍然是当前写作协作规则的权威位置；本页和下游 wiki assets 负责把这些规则提升成可连接、可修订的理论资产。

本 source note 不复制 profile 原文，只提炼它对理论系统的贡献。

## 核心贡献

`profile/writing/` 提供了一套关于 agent-facing 文档的理论雏形：

- Markdown 文档应被视为 [document module](../concepts/document-module.md)。
- 文档内部可以分为 [document metadata](../concepts/document-metadata.md)、[assertion](../concepts/assertion.md) 和结构化正文。
- 面向 agent 的规范应优先使用 [agent-facing pattern](../concepts/agent-facing-pattern.md)，而不是只依赖描述性散文。
- 指令强度应使用 [normative keyword](../concepts/normative-keyword.md) 分层表达。
- 文档结构会训练未来维护行为，见 [Document structure trains maintenance](../claims/document-structure-trains-maintenance.md)。

## 提炼资产

Concepts：

- [Document Module](../concepts/document-module.md)
- [Document Metadata](../concepts/document-metadata.md)
- [Assertion](../concepts/assertion.md)
- [Agent-facing Pattern](../concepts/agent-facing-pattern.md)
- [Normative Keyword](../concepts/normative-keyword.md)

Claims：

- [Agent-facing docs need patterns, not descriptions alone](../claims/agent-docs-need-patterns-not-descriptions.md)
- [Document structure trains maintenance](../claims/document-structure-trains-maintenance.md)
- [Strong constraints should be scarce](../claims/strong-constraints-should-be-scarce.md)

Patterns：

- [Assertion-level Review](../patterns/assertion-level-review.md)
- [Frontmatter for Persistent State](../patterns/frontmatter-for-persistent-state.md)
- [Normative Keyword Ladder](../patterns/normative-keyword-ladder.md)
- [Split Index Document Architecture](../patterns/split-index-document-architecture.md)

Examples：

- [Vocabulary Entry as Assertion](../examples/vocabulary-entry-as-assertion.md)
- [Next.js Docs Constraint Assertion](../examples/nextjs-docs-constraint-assertion.md)
