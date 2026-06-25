---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义通过函数签名暴露成功值、失败通道和依赖能力的工程边界。
type: concept
status: active
confidence: medium
sources:
  - ../sources/effect-without-effect-ts.md
updated: 2026-06-25
---

# Effectful Function Signature

## 定义

Effectful function signature 是把一次操作的业务输入、依赖能力、异步性、成功值和失败类型都表达在类型签名中的函数边界。

它反对让 `Promise<T>`、throwing 和 module-level imports 隐藏操作的真实行为。调用者应该能从签名看出这个函数需要哪些能力、会产生哪些可预期失败，以及成功时返回什么。

## 边界

这个概念不要求采用 Effect-TS 或任何 effect framework。它描述的是函数边界的诚实程度，不是某个库的 API 风格。

并非每个纯计算函数都需要这种签名。它主要适用于会触碰外部系统、校验输入、跨模块传播错误或需要在测试中替换依赖的操作。

## 关系

[Explicit Effects in Plain TypeScript](../patterns/explicit-effects-in-plain-typescript.md) 是在 TypeScript 中实现 effectful function signature 的一个模式。

[Plain TypeScript Can Carry Algebraic Effect Ideas](../claims/plain-typescript-can-carry-algebraic-effect-ideas.md) 说明这个概念可以脱离完整 framework 独立采用，但会遇到组合和并发语义的规模边界。
