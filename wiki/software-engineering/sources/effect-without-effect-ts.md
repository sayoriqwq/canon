---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 消化 Effect Without Effect-TS，并连接 plain TypeScript 中显式错误、显式依赖和组合边界的工程理论资产。
type: source
status: active
confidence: medium
sources: []
raw:
  - ../../../raw/articles/Effect Without Effect-TS Algebraic Thinking in Plain TypeScript.md
updated: 2026-06-25
---

# Effect Without Effect-TS Source Note

## Source 边界

本页消化 Christian Ekrem 的文章《Effect Without Effect-TS: Algebraic Thinking in Plain TypeScript》。Raw source 仍然是文章原文的权威位置；本页只记录它对 software-engineering sub-wiki 的理论贡献。

本 source note 不复制文章正文或教程代码，只提炼可连接、可修订的 durable assertions。

## 核心贡献

这篇文章把 Effect-TS 背后的部分想法拆成可以在 plain TypeScript 中独立采用的工程结构：

- 把失败作为显式值返回，让错误通道进入函数签名。
- 把数据库、邮件、分析等外部能力作为依赖参数传入，让操作需要的能力进入函数签名。
- 用小型组合 helper 可以缓解顺序 `Result` 流程的样板，但深层组合、跨模块错误合并和 structured concurrency 会暴露 plain TypeScript 的表达力边界。
- Effect-TS 的价值不只在理念本身，也在当这些理念规模化后提供可维护的组合语法、运行时模型和并发语义。

## 提炼资产

Concepts：

- [Effectful Function Signature](../concepts/effectful-function-signature.md)

Claims：

- [Plain TypeScript Can Carry Algebraic Effect Ideas](../claims/plain-typescript-can-carry-algebraic-effect-ideas.md)

Patterns：

- [Explicit Effects in Plain TypeScript](../patterns/explicit-effects-in-plain-typescript.md)
