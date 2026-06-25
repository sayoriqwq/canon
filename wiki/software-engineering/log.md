---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 software-engineering sub-wiki 维护历史，包括 source ingest、理论页修订和 lint。
updated: 2026-06-25
---

# Software Engineering Log

这里记录 software-engineering sub-wiki 的 source ingest、理论页面创建或修订、synthesis 更新和 lint。

## 记录

- 2026-06-24：创建 `wiki/software-engineering/concepts/assertion.md`，将 assertion 引入为文档迭代中的最小语义单元，并补充术语表词条也是 assertion 结构；更新 `wiki/software-engineering/concepts/index.md` 和 `wiki/vocabulary/agent/index.md`。
- 2026-06-24：把 `wiki/profile/writing/` 作为内部 source 消化到 software-engineering sub-wiki，创建 `wiki/software-engineering/sources/profile-writing.md`，新增 document module、document metadata、agent-facing pattern、normative keyword 等 concepts，新增相关 claims、patterns、examples，并更新当前 synthesis。
- 2026-06-25：作为 canon wiki federation 重构的一部分，从根 `wiki/` 迁入 `wiki/software-engineering/`。
- 2026-06-25：收窄 `assertion` 和 `normative keyword` concept 页的职责，把词义边界指回 `wiki/vocabulary/agent/index.md`；将 source note 复制约束移入 `HARNESS.md`。
- 2026-06-25：摄入 raw article `raw/articles/Effect Without Effect-TS Algebraic Thinking in Plain TypeScript.md`，创建 `wiki/software-engineering/sources/effect-without-effect-ts.md`，新增 effectful function signature concept、explicit effects in plain TypeScript pattern 和 plain TypeScript can carry algebraic effect ideas claim，并更新当前 synthesis。
