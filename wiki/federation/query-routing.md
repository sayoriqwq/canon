---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义用户只问 canon 时 agent 如何在 sub-wiki 之间路由读取。
type: pattern
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Query Routing

用户不需要指定 sub-wiki。

Agent 回答 canon 问题时，先读 `wiki/index.md`，再根据问题选择 candidate sub-wiki。

## 流程

```text
user question
  -> wiki/index.md
  -> candidate sub-wiki indexes
  -> relevant pages
  -> answer with ownership boundary
```

## 读取规则

Read can be federated。

一个问题可以读取多个 sub-wiki。例如“文档维护应该怎么做”可能同时读取 `wiki/profile/` 的偏好、`wiki/software-engineering/` 的模式和 `wiki/vocabulary/` 的术语。

回答时应区分依据：哪些是用户偏好，哪些是泛化理论，哪些是术语定义。
