---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 plain TypeScript 可以承载部分 effect 思想但会遇到组合边界的判断。
type: claim
status: active
confidence: medium
sources:
  - ../sources/effect-without-effect-ts.md
updated: 2026-06-25
---

# Plain TypeScript Can Carry Algebraic Effect Ideas

## 判断

Plain TypeScript 可以独立承载 typed errors、explicit dependencies 和顺序结果组合等 algebraic thinking，不必为了这些单点收益立即引入完整 Effect-TS。

完整 effect framework 的主要增量价值会在组合规模、错误映射、资源生命周期和 structured concurrency 上显现，而不是在“错误作为值”或“依赖作为参数”这些基础思想本身。

## 支持

`Result` 类型、discriminated union、依赖参数和小型组合 helper 已经能让函数签名更诚实，并改善测试替身的注入方式。

但 TypeScript 缺少原生 computation expression 或 `do` notation。随着调用链加深，手写组合会产生样板和嵌套，跨模块错误 union 也会变得需要人工维护。

## 连接

- [Effectful Function Signature](../concepts/effectful-function-signature.md)
- [Explicit Effects in Plain TypeScript](../patterns/explicit-effects-in-plain-typescript.md)
