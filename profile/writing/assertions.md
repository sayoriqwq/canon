---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 保存 sayori 关于按 assertion 识别、审查和修改 Markdown 文档的协作规则。
updated: 2026-06-24
---

# Assertion 协作规则

## 核心判断

Markdown 文档由多条 assertion 组成。

Assertion 是文档迭代时被识别和审查的最小**语义单元**。agent 修改文档时，SHOULD 先判断当前变更是在新增、修订、拆分、合并、挑战还是移除哪条 assertion。

## Assertion 边界

Assertion 不等同于一句话。

一句自然语言可能包含多条 assertion；一条 assertion 也可能跨越多句。判断标准是它是否表达了一个独立的事实、约束、解释、偏好或判断。

## 协作规则

- SHOULD 以 assertion 为最小审查单位，而不是只按段落、章节或整页印象审查。
- SHOULD 在语义密集文档中说明本次改动影响了哪些 assertion。
- SHOULD 优先修改发生变化的最小 assertion，避免重写未变化的相邻内容。
- MUST NOT 把自然句边界当成可靠的 assertion 边界。
- MUST NOT 因为文档标题或段落主题看起来正确，就跳过其中具体 assertion 的检查。

## 词条也是 Assertion

术语表词条是一种紧凑的 assertion 结构：

```md
`term`
: definition
_Avoid_: confusing terms
```

其中 `term` 是 assertion 的对象，`definition` 是关于该对象边界的主 assertion。可选的 `_Avoid_` 是负向边界 assertion，用来拒绝容易混淆的同义词或过载词。

因此，维护 vocabulary 时不是只在整理词名，而是在维护一组关于概念边界的 assertion。

## 示例

Next.js 项目中的一句约束可以是一条 assertion：

```text
本项目使用 Next.js 16，相关 API 可能不同于模型训练数据，需要读取本地 `node_modules/next/dist/docs/`。
```
