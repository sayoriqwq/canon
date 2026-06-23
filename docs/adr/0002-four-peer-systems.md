---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 canon 初始四系统架构及其被 vocabulary 系统取代的历史。
updated: 2026-06-24
status: superseded by ADR-0007
---

# ADR-0002: 四个并列系统

## 背景

Canon 需要处理未裁决 fragments、被保存的原始材料、消化后的理论资产和当前用户上下文，同时 MUST NOT 混合它们的生命周期。

## 决策

Canon 最初有四个并列系统：

- `fragments/`：权威 fragment 裁决。
- `raw/`：被保存的原始材料。
- `wiki/`：消化后的理论资产。
- `profile/`：当前用户和协作模型。

## 后果

每个系统都有自己的 index 和维护规则。MUST NOT 把这些层折叠成一个 notes 目录。

ADR-0007 已增加 `vocabulary/` 作为第五个并列系统。
