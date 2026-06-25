---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 展示一条项目约束如何作为 assertion 被审查。
type: example
status: active
confidence: medium
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Next.js Docs Constraint Assertion

## 例子

```text
本项目使用 Next.js 16，相关 API 可能不同于模型训练数据，需要读取本地 `node_modules/next/dist/docs/`。
```

这是一条 [assertion](../concepts/assertion.md)：它表达了项目版本、模型知识风险和本地文档读取要求之间的约束。

## 可审查点

这条 assertion 后续可以被更新：

- 如果项目升级版本，修改版本部分。
- 如果本地文档路径变化，修改读取位置。
- 如果模型知识风险被新的检索机制替代，修改审查要求。
