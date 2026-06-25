---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 说明 assertion 在文档维护理论中的作用。
type: concept
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-25
---

# 断言 Assertion

## 理论使用

`assertion` 的词义边界由 [Agent 术语表](../../vocabulary/agent/index.md) owning。本页只说明 assertion 在文档维护理论中的作用。

一份 Markdown 文档由多条 assertion 组成。迭代文档时，agent 审查的对象不是整份文档的模糊印象，而是一条条可以成立、过期、冲突、拆分或合并的 assertion。

## 边界

这里的 assertion 不是测试框架里的 assert，也不是形式逻辑中的完整命题系统。它是面向文档维护的语义单位。

一句自然语言可能包含多条 assertion；一条 assertion 也可能跨越多句。判断标准是它是否表达了一个独立的约束、事实、解释或判断。

## 示例

Next.js 项目中的一句约束可以是一条 assertion：

> 本项目使用 Next.js 16，相关 API 可能不同于模型训练数据，需要读取本地 `node_modules/next/dist/docs/`。

术语表词条也是一种 assertion 结构。`term` 是被定义对象，定义行是关于该对象语义边界的主 assertion，`_Avoid_` 是可选的负向边界 assertion。

## 关系

Assertion 是 [Document Module](document-module.md) 的语义层。对 assertion 的修改应使用 [Assertion-level Review](../patterns/assertion-level-review.md)。

具体实例见 [Vocabulary Entry as Assertion](../examples/vocabulary-entry-as-assertion.md) 和 [Next.js Docs Constraint Assertion](../examples/nextjs-docs-constraint-assertion.md)。
