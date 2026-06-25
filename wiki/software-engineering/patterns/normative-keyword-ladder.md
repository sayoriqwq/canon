---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 描述用分层指令强度词约束 agent 行为的模式。
type: pattern
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Normative Keyword Ladder

## 模式

使用少量固定 [normative keyword](../concepts/normative-keyword.md) 表达指令强度：

- `MUST` / `MUST NOT`：强约束。
- `SHOULD` / `SHOULD NOT`：默认策略，可有理由地偏离。
- `MAY`：开放空间。

## 适用场景

当一份规范需要同时表达不可违反规则、默认偏好和可选路径时，使用这个分层，而不是把所有要求写成同一种语气。

## 约束

强约束应遵守 [Strong constraints should be scarce](../claims/strong-constraints-should-be-scarce.md)。
