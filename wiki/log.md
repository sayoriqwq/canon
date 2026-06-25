---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 canon wiki federation 级别的维护历史。
updated: 2026-06-25
---

# Wiki Federation Log

## 记录

### 2026-06-25 | restructure | Canon as wiki federation

- 将 `profile/` 迁入 `wiki/profile/`。
- 将 `vocabulary/` 迁入 `wiki/vocabulary/`。
- 将原 `wiki/` 理论资产迁入 `wiki/software-engineering/`。
- 移除根目录 `fragments/`，canon 不再维护长期 fragment inbox。
- 新增 `wiki/federation/` 作为 canon 自己的 wiki federation 理论 sub-wiki。

### 2026-06-25 | lint | Vocabulary ownership cleanup

- 收窄 `wiki/vocabulary/profile/index.md` 的 `current profile` 词条，避免在 vocabulary 定义中承载 profile 维护流程。
- 将 vocabulary 分层规则和词条格式约束移入 `HARNESS.md`，让 `wiki/vocabulary/index.md` 回到 sub-wiki 入口职责。
