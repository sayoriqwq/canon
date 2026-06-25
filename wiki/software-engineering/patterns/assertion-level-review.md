---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 描述按 assertion 审查和修改文档的模式。
type: pattern
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Assertion-level Review

## 模式

修改文档时，先识别本次变更影响了哪些 [assertion](../concepts/assertion.md)，再决定新增、修订、拆分、合并、挑战或移除。

不要只按句子、段落、章节或整页印象审查。

## 适用场景

- 语义密集的规范文档。
- 长期维护的 profile、harness、ADR 或 wiki 页面。
- 需要避免重写未变化相邻内容的编辑任务。

## 例子

- [Vocabulary Entry as Assertion](../examples/vocabulary-entry-as-assertion.md)
- [Next.js Docs Constraint Assertion](../examples/nextjs-docs-constraint-assertion.md)
