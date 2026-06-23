---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 说明 canon 的仓库意义、边界、系统层级和核心反馈回路。
updated: 2026-06-24
---

# Canon 上下文

## 目的

Canon 是个人软件工程理论系统。

它服务于 `profile/` 中描述的用户：一个围绕现代软件系统建设长期理解的开发者。

目标不是收集笔记，而是把学习输入编译成持久的工程判断。

## 非目标

Canon 不是：

- 项目任务追踪器。
- prompt snippet dump。
- 仓库专属 coding rule 集合。
- 通用技术 taxonomy。
- 永久保存每个有趣 fragment 的地方。
- 替代具体实践仓库的地方。

实践发生在具体仓库中。Canon 只在实践被抽象成可复用理解后保存理论。

## 核心反馈回路

本系统服务于这个循环：

```text
material or fragment
  -> capture
  -> judge
  -> digest
  -> connect
  -> revise current understanding
  -> improve future reading, coding, and agent collaboration
```

如果某个变更不能改善这个循环，SHOULD 把它视为可疑变更。

## 系统层级

Canon 是 single-context 仓库，不使用 `CONTEXT-MAP.md`。

仓库有五个并列系统：

- `fragments/`：权威碎片裁决系统。
- `raw/`：按材料形态保存的原始材料。
- `wiki/`：消化后的理论资产。
- `profile/`：跨目录仍然有效的当前用户上下文和偏好。
- `vocabulary/`：跨目录有效的分层术语表。

它们是同一个系统的不同层，不是彼此独立的 domain context。

## 术语表

完整术语表在 `vocabulary/` 中维护。`CONTEXT.md` 不保留核心术语副本，避免两处定义漂移。

维护或查询术语时，进入 [Vocabulary](vocabulary/index.md)。

## 架构原则

- SHOULD 偏好单一职责文档。
- SHOULD 从一开始使用 split index architecture，即使仓库还小。
- MUST NOT 因为文件少就保留一个巨大的 index。
- MUST NOT 让 fragments 变成永久理论资产。
- MUST NOT 把 raw 原始材料直接放进理论页面。
- MUST NOT 在 `profile/` 中保留过期偏好。
- MUST NOT 把 canon 仓库决策提升进 `wiki/`，除非用户明确要求把它泛化成软件工程理论。
- MUST NOT 把 glossary 副本放回 `CONTEXT.md`；分层术语使用 `vocabulary/`。
