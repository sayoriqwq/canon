---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 保存 software-engineering sub-wiki 当前高层 synthesis，连接已有理论资产。
type: synthesis
status: active
confidence: medium
sources:
  - ../sources/effect-without-effect-ts.md
  - ../sources/profile-writing.md
updated: 2026-06-25
---

# 当前 Synthesis

当前 software-engineering sub-wiki 的第一组理论资产来自 [Profile Writing](../sources/profile-writing.md)。

## 文档即可维护模块

Markdown 文档不只是文本容器，而是 [document module](../concepts/document-module.md)。它需要稳定职责、索引入口、metadata、assertion 和结构化正文，才能被长期维护。

## Agent-facing 文档需要模式

面向 agent 的文档应优先使用 [agent-facing pattern](../concepts/agent-facing-pattern.md)。描述负责解释意图，模式负责给出可执行边界。

关键模式包括：

- [Frontmatter for Persistent State](../patterns/frontmatter-for-persistent-state.md)
- [Assertion-level Review](../patterns/assertion-level-review.md)
- [Normative Keyword Ladder](../patterns/normative-keyword-ladder.md)
- [Split Index Document Architecture](../patterns/split-index-document-architecture.md)

## 操作签名应暴露 effect 边界

来自 [Effect Without Effect-TS](../sources/effect-without-effect-ts.md) 的当前判断是：TypeScript 中的 effectful operation 不应只暴露 `Promise<T>`。

[Effectful Function Signature](../concepts/effectful-function-signature.md) 要求函数边界表达成功值、失败通道和依赖能力。[Explicit Effects in Plain TypeScript](../patterns/explicit-effects-in-plain-typescript.md) 是不引入完整 framework 时的可用模式；[Plain TypeScript Can Carry Algebraic Effect Ideas](../claims/plain-typescript-can-carry-algebraic-effect-ideas.md) 则保留了它的规模边界。

## 维护行为由结构塑造

当前核心判断是：[Document Structure Trains Maintenance](../claims/document-structure-trains-maintenance.md)。文档结构会影响后续 agent 如何判断边界、入口和允许的改动方式。
