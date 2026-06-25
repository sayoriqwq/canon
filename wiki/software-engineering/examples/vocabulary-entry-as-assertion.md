---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 展示术语表词条如何构成 assertion。
type: example
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Vocabulary Entry as Assertion

## 例子

术语表词条是一种紧凑的 [assertion](../concepts/assertion.md) 结构：

```md
`term`
: definition
_Avoid_: confusing terms
```

`term` 是 assertion 的对象，`definition` 是关于该对象语义边界的主 assertion。`_Avoid_` 是可选的负向边界 assertion。

## 作用

维护 vocabulary 不是只整理词名，而是在维护一组关于概念边界的 assertion。

## 连接

- [Assertion-level Review](../patterns/assertion-level-review.md)
- [Agent-facing Pattern](../concepts/agent-facing-pattern.md)
