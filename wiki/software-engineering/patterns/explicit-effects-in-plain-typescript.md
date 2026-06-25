---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 描述在 plain TypeScript 中显式表达错误、依赖和异步操作的模式。
type: pattern
status: active
confidence: medium
sources:
  - ../sources/effect-without-effect-ts.md
updated: 2026-06-25
---

# Explicit Effects in Plain TypeScript

## 模式

在 TypeScript 的 effectful operation 边界，用 `Promise<Result<T, E>>` 暴露异步成功值和失败通道，用 discriminated union 表达可预期错误，用依赖对象或函数参数暴露外部能力。

生产环境在系统边缘组装真实依赖；测试直接传入 fake dependencies。业务函数不从 module-level imports 偷拿数据库、邮件服务或 analytics client。

## 适用场景

- 操作会访问数据库、网络、文件系统、队列、邮件或第三方服务。
- 调用者需要区分 validation、domain、infrastructure 等不同失败。
- 测试需要替换外部能力，而不依赖 mocking library 或全局 patch。
- 团队暂时不想引入完整 effect framework，但希望先获得 typed errors 和 explicit dependencies 的收益。

## 约束

当流程超过少量顺序步骤时，手写 `Result` 组合会快速变啰嗦。可以先用小型 helper 合并样板；如果组合、错误映射、资源生命周期或 structured concurrency 成为核心复杂度，应该重新评估是否需要 Effect-TS 或同类框架。

## 连接

- [Effectful Function Signature](../concepts/effectful-function-signature.md)
- [Plain TypeScript Can Carry Algebraic Effect Ideas](../claims/plain-typescript-can-carry-algebraic-effect-ideas.md)
