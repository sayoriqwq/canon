---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 fragment 裁决类型、提升标准和 provenance 规则。
updated: 2026-06-24
---

# Fragment 规则

## 目的

Fragments 只为裁决而存在。它们 MUST NOT 变成永久的并行知识库。

## 裁决类型

- `promote-to-wiki`：把 fragment 转成 wiki asset，或用它修订 wiki asset。
- `update-profile`：更新当前用户或上下文模型。
- `preserve-raw`：把原始材料捕获到 `raw/`。
- `hold-once`：只推迟一次。
- `archive`：保留用于 audit，但不提升。
- `discard`：从活跃考虑中移除。

## 提升标准

Fragment 只有至少完成一个理论功能，MAY 进入 wiki：

- `explain`：澄清一个 concept。
- `question`：产生一个 durable question。
- `support`：增强一个 claim。
- `challenge`：削弱或复杂化一个 claim。
- `generalize`：成为可复用 pattern。
- `revise`：改变 synthesis。

## Hold 规则

`hold-once` MUST NOT 重复。下一次 review MUST 选择最终 verdict。

## Provenance 规则

Wiki pages MUST NOT 添加 fragment backlinks。提升后，fragment 的活跃身份消失。

Review 后，MUST 从活跃 inbox/review 文件中移除已裁决 fragments。只有仍有 audit 价值时，MAY 把 fragment 正文保存在 `archive/`。
