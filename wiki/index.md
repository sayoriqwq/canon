---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 作为 canon wiki federation map，帮助 agent 路由到正确 sub-wiki。
updated: 2026-06-25
---

# Wiki Federation

`wiki/` 是 canon 的唯一长期知识主体。它对用户表现为一个整体；对 agent 维护时拆成多个 sub-wiki。

Sub-wiki 是 assertion ownership 区域。用户不需要指定 sub-wiki；agent MUST 根据问题和写回内容路由。

## Sub-wiki

- [Federation](federation/index.md)：canon 自己的 wiki federation 理论。
- [Profile](profile/index.md)：当前用户模型、偏好和协作语义。
- [Vocabulary](vocabulary/index.md)：跨 sub-wiki 共享术语、关系语义和边界。
- [Software Engineering](software-engineering/index.md)：软件工程和 agent-facing 文档理论资产。

## Federation 文件

- [Log](log.md)：federation-level 维护日志。

## 路由原则

Read can be federated; write must be owned.

一个问题可以读取多个 sub-wiki。写回 durable assertion 时，必须选择一个 owning sub-wiki，并通过 cross-link 连接相关页面。
