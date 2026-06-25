---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 保存 agent 协作和指令规范相关术语。
updated: 2026-06-25
---

# Agent 术语表

## 词条

`agent`
: 读取上下文、执行任务、维护文档或代码的模型执行者。

`prompt`
: 一次性模型输入，用于约束当前任务的目标、输入、输出、语气、步骤和验收条件。

`frontmatter`
: Markdown 文件顶部的结构化 metadata block，用于保存文档级别的持久状态。

`metadata`
: 机器可读的文档状态信息，例如 `audience`、`authors`、`reviewed_by`、`purpose`、`updated`。

`audience`
: 文档 metadata 中的读者类型，只描述 `agent`、`human` 或二者列表。

`authors`
: 文档 metadata 中的生成或主要撰写者列表。

`reviewed_by`
: 文档 metadata 中明确 review 或批准过该文档的人。

`purpose`
: 文档 metadata 中的一句话用途说明，描述读者打开这份文档要完成什么。

`normative keyword`
: 表达指令强度的关键词，例如 `MUST`、`MUST NOT`、`SHOULD`、`SHOULD NOT`、`MAY`。

`input pattern`
: agent 应如何读取信息的稳定结构，例如固定字段、枚举值、目录命名、模板变量。

`output pattern`
: agent 应如何生成结果的稳定结构，例如固定章节、必填字段、状态流转格式、检查清单格式。

`assertion`
: 文档迭代时被识别和审查的最小语义单元。一份 Markdown 文档由多条 assertion 组成。
_Avoid_: 测试断言、形式逻辑命题
