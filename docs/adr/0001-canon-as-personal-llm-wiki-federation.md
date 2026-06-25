---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 canon 采用 personal LLM-wiki federation 架构的决策。
updated: 2026-06-25
status: accepted
---

# ADR-0001: Canon 作为 Personal LLM-wiki Federation

## 背景

旧架构把 `fragments/`、`raw/`、`wiki/`、`profile/` 和 `vocabulary/` 描述为并列系统。这会让 agent 误以为 canon 是多个知识系统的聚合，并可能为同一条 assertion 建立多个真源。

当前核心参照是根目录 [LLM Wiki](../../llm-wiki.md)。Canon 应实例化这个模式：LLM 持续维护一个持久、互联、会复利增长的 Markdown wiki，而不是在多个并列系统之间搬运内容。

## 决策

Canon 是一个 personal LLM-wiki federation。

`wiki/` 是唯一长期知识主体。`profile`、`vocabulary`、软件工程理论和 wiki federation 理论都作为 `wiki/` 下的 sub-wiki 维护。

当前结构：

```text
raw/                     # source layer, not wiki
wiki/
  federation/            # canon wiki federation theory
  profile/               # user model and preferences
  vocabulary/            # shared terms and relation semantics
  software-engineering/  # software engineering theory
```

`raw/` 保留为非 wiki 的原始材料层。

`fragments/` 不属于 canon。Canon 不维护长期 fragment inbox、review backlog 或 prompt dump。

## 不变量

```text
read can be federated
write must be owned
links can cross sub-wiki
assertions cannot have duplicate owners
```

Sub-wiki 是 assertion ownership 区域，不是主题文件夹。

每条 durable assertion 只能有一个 owning sub-wiki 或 raw source。其它位置只能链接、引用、摘要、派生、泛化或投影。

## 后果

根目录 MUST NOT 恢复 `profile/`、`vocabulary/` 或 `fragments/`。

Agent 回答 canon 问题时，先读取 `wiki/index.md`，再路由到 candidate sub-wiki。用户不需要显式指定 sub-wiki。

架构理论写入 `wiki/federation/`；操作协议写入 `HARNESS.md`；仓库决策写入 ADR。

明显 breaking 的旧 ADR 不保留为 superseded 文件，避免新 agent 读取过期模型。
