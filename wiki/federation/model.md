---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 canon wiki federation 的整体模型。
type: synthesis
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Federation Model

Canon 是一个 personal LLM-wiki federation。

它继承 [LLM Wiki](../../llm-wiki.md) 的核心模式：LLM 不在每次 query 时重新拼接 raw chunks，而是持续维护一个持久、互联、会复利增长的 Markdown wiki。

## Canon 实例化

Canon 的长期知识主体只有 `wiki/`。

`wiki/` 内部按 assertion ownership 拆分成 sub-wiki：

- `federation`：canon wiki federation 理论。
- `profile`：当前用户模型、偏好和协作语义。
- `vocabulary`：跨 sub-wiki 共享术语和关系语义。
- `software-engineering`：软件工程和 agent-facing 文档理论。

`raw/` 是 source layer，不是 sub-wiki。

Schema 层由 `AGENTS.md`、`CONTEXT.md`、`HARNESS.md` 和 ADR 组成，不是 wiki 内容层。

## 核心判断

Wiki federation 不是多个并列系统的集合。它是一个 wiki，由多个 ownership 区域协同维护。

用户可以只问 canon；agent 负责读取 federation map，选择相关 sub-wiki，并在需要写回时确定唯一 owner。
