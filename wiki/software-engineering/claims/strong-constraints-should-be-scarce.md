---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录强约束应稀缺使用的判断。
type: claim
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Strong Constraints Should Be Scarce

## 判断

强约束应稀缺使用。

`MUST` 和 `MUST NOT` 应保留给安全边界、文件职责边界、可检查格式、长期上下文污染风险，以及后续 agent 难以恢复的错误。

## 支持

强约束过多会让 agent 难以判断真正不可违反的边界。风格偏好、常规建议和可替代方案更适合使用 `SHOULD`、`SHOULD NOT` 或 `MAY`。

## 连接

- [Normative Keyword](../concepts/normative-keyword.md)
- [Normative Keyword Ladder](../patterns/normative-keyword-ladder.md)
