---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 说明 canon 作为 personal LLM-wiki federation 的仓库意义、边界和顶层架构。
updated: 2026-06-25
---

# Canon 上下文

## 目的

Canon 是一个 personal LLM-wiki federation。

它以 [LLM Wiki](llm-wiki.md) 为原始参照：LLM 不只在 query 时检索原始材料，而是持续建立、维护和查询一个持久、互联、会复利增长的 Markdown wiki。

Canon 的目标不是保存零散笔记，也不是维护多个并列知识系统，而是让长期有效的知识、偏好、术语和理论都进入 `wiki/` 下的 federation，并通过明确的 sub-wiki ownership 保持唯一真源。

## 顶层架构

Canon 只有一个长期知识主体：

```text
wiki/
```

`wiki/` 是 federated wiki。它对用户表现为一个整体；对 agent 维护时拆成多个 sub-wiki。Sub-wiki 是 assertion ownership 区域，不是要求用户显式指定的入口。

当前 sub-wiki：

- `wiki/federation/`：canon 自己的 wiki federation 理论。
- `wiki/profile/`：当前用户模型、偏好和协作语义。
- `wiki/vocabulary/`：跨 sub-wiki 共享术语、关系语义和边界。
- `wiki/software-engineering/`：软件工程理论资产。

非 wiki 层：

- `raw/`：原始材料层，只服务来源保真，不承载综合理解。
- `AGENTS.md`、`CONTEXT.md`、`HARNESS.md`、`docs/adr/`：schema 和仓库治理层，规定 agent 如何维护 federation。
- `llm-wiki.md`：外部原始参照，不是 canon 自己的理论展开。

## 核心不变量

Read can be federated; write must be owned.

一个问题可以读取多个 sub-wiki；写回时必须选择明确的 owning sub-wiki。

每条 durable assertion 只能有一个 owning sub-wiki 或 raw source。其他位置只能链接、引用、摘要、派生、泛化或投影，不能复制成第二真源。

Sub-wiki 按 assertion ownership 拆分，不按主题词拆分。判断页面归属时，看它主张的 assertion 类型，而不是它提到了哪些主题。

## 反馈回路

Canon 服务这个循环：

```text
source or conversation
  -> route
  -> read owning and related sub-wikis
  -> answer or ingest
  -> write durable assertions to one owning sub-wiki
  -> update cross-links, index, and log
  -> lint duplicate truth, stale links, and missing connections
```

如果某个变更不能改善这个循环，SHOULD 把它视为可疑变更。

## 非目标

Canon 不是：

- 项目任务追踪器。
- prompt snippet dump。
- 临时 fragment inbox。
- 仓库专属 coding rule 集合。
- 原始材料解释层。
- 多个并列系统的聚合目录。
- 每个有趣 fragment 的永久保存地。

未被编译进 owning sub-wiki 的临时想法不在 canon 内长期保存。

## 架构原则

- MUST 让 `wiki/` 成为唯一长期知识主体。
- MUST 把 `profile`、`vocabulary` 和软件工程理论都建模为 `wiki/` 下的 sub-wiki。
- MUST NOT 在根目录恢复 `profile/`、`vocabulary/` 或 `fragments/` 作为并列系统。
- MUST 保持 `raw/` 为非 wiki 的原始材料层。
- MUST 保持每条 durable assertion 的唯一 owner。
- MUST 让用户可以只问 canon，由 agent 负责 query routing。
- SHOULD 使用 split index architecture：根 `index.md` 指向顶层入口，`wiki/index.md` 指向 sub-wiki，每个 sub-wiki 的 `index.md` 只列下一层。
- SHOULD 把 wiki federation 理论写入 `wiki/federation/`，把维护规则写入 `HARNESS.md`，把仓库决策写入 `docs/adr/`。
