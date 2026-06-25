---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 canon wiki federation 的健康检查规则。
type: pattern
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Lint Rules

Lint 的目标是保持 canon 作为 wiki federation，而不是退回多个并列系统或散乱笔记库。

## 检查项

- 根目录没有 `profile/`、`vocabulary/`、`fragments/`。
- `wiki/index.md` 列出的 sub-wiki 和实际目录一致。
- 每个 sub-wiki 有本地 `index.md`。
- 同一 durable assertion 没有多个 owners。
- Cross-link 没有指向迁移前旧路径。
- `raw/` 原文没有被解释化或重排。
- `wiki/profile/` 没有 deprecated 偏好。
- `wiki/vocabulary/` 没有混入操作流程或实现 spec。
- `wiki/federation/` 保存理论，不保存操作守则。
- `HARNESS.md` 保存操作守则，不展开理论。
