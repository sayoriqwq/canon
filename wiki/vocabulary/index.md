---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 作为 vocabulary sub-wiki 入口，帮助 agent 找到跨 sub-wiki 共享术语和关系语义。
updated: 2026-06-25
---

# Vocabulary

`wiki/vocabulary/` 是 canon 的 vocabulary sub-wiki。

它 owns 跨 sub-wiki 共享的术语、关系语义和边界。它不是根目录并列系统，也不是 `CONTEXT.md` 的 glossary 副本。

## 分层规则

优先按术语服务的语义边界分层，而不是按抽象程度分层。

如果一个术语主要服务 canon 和 wiki federation，就放入 `canon/`。

如果一个术语主要服务 agent 协作、指令规范、模型输入输出约束，就放入 `agent/`。

如果一个术语主要服务用户模型和偏好维护，就放入本 sub-wiki 的 `profile/` 区域。

当某个 sub-wiki 的共享术语规模变大，MAY 新增专门区域；MUST NOT 提前创建空目录。

## 词条格式

词条使用统一格式：

```md
`term`
: 一到两句话定义。只说它是什么，不展开操作流程。
_Avoid_: 误用词 A、误用词 B
```

`_Avoid_` 是可选字段，只在确实有混淆词时使用。

定义要短，优先说明概念边界，不写实现细节，不写维护流程。

## 区域

- [Canon](canon/index.md)：canon 和 wiki federation 术语。
- [Agent](agent/index.md)：agent 协作和指令规范术语。
- [Profile](profile/index.md)：用户模型和偏好维护术语。
