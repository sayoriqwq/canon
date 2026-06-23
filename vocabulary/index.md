---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 作为 vocabulary 系统入口，帮助 agent 找到跨目录术语表。
updated: 2026-06-24
---

# 术语表

`vocabulary/` 保存跨目录有效的术语表。它不是某个单页 glossary，而是和 `profile/` 类似的全局系统。

`vocabulary/` 是术语定义的权威位置。`CONTEXT.md` 只指向这里，不保留小型术语副本。

术语按使用场景和语义层级拆分到不同目录。MUST NOT 把所有术语塞回 `CONTEXT.md`。

## 分层规则

优先按术语服务的系统边界分层，而不是按抽象程度分层。

如果一个术语主要服务 canon 仓库和知识系统，就放入 `canon/`。

如果一个术语主要服务 agent 协作、指令规范、模型输入输出约束，就放入 `agent/`。

如果一个术语主要服务用户画像和偏好维护，就放入 `profile/`。

当 wiki 理论体系中的术语规模变大，MAY 新增专门区域；MUST NOT 提前创建空目录。

## 词条格式

词条使用统一格式：

```md
`term`
: 一到两句话定义。只说它是什么，不展开操作流程。
_Avoid_: 误用词 A、误用词 B
```

`_Avoid_` 是可选字段，只在确实有混淆词时使用。

定义要短，优先说明概念边界，不写实现细节，不写维护流程。

多个词 MAY 按自然主题增加小标题；如果一个区域内术语仍然集中，MAY 保持单一 `## 词条`。

## Agent 路由

`vocabulary/` 暂时 MUST NOT 加入 `AGENTS.md` 默认路由。

等第一轮核心词表稳定后，再让 `AGENTS.md` 直接引入 `vocabulary/index.md`。

## 区域

- [Canon](canon/index.md)：canon 仓库和知识系统术语。
- [Agent](agent/index.md)：agent 协作和指令规范术语。
- [Profile](profile/index.md)：用户画像和偏好维护术语。
