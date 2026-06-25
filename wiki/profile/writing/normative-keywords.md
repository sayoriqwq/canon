---
audience: agent
authors:
  - codex
reviewed_by: []
purpose: 保存 sayori 对 agent 指令强度词的偏好。
updated: 2026-06-24
---

# 指令强度词

## 核心判断

面向 agent 的规范应使用清晰的指令强度词，避免把所有要求都写成同一种语气。

这里借鉴 RFC 2119 的语义层级：强约束、次强约束、允许模型发挥。目标不是让文字显得正式，而是让 agent 能判断哪些规则不可违反，哪些规则允许有理由地偏离，哪些只是可选路径。

## 关键词

本 profile 优先使用以下五组关键词：

| 关键词 | 强度 | 含义 |
| --- | --- | --- |
| `MUST` | 强约束 | 必须执行。除非和更高优先级指令冲突或现实条件阻塞，否则违反就是错误。 |
| `MUST NOT` | 强约束 | 禁止执行。除非和更高优先级指令冲突，否则不能做。 |
| `SHOULD` | 次强约束 | 默认应该执行。可以偏离，但必须有具体理由。 |
| `SHOULD NOT` | 次强约束 | 默认不应该执行。可以偏离，但必须理解并说明代价。 |
| `MAY` | 模型发挥 | 允许执行，但不是义务。 |

RFC 2119 还包含 `REQUIRED`、`SHALL`、`RECOMMENDED`、`OPTIONAL` 等同义表达。为减少 agent 解析噪声，本 profile 默认只使用上表五组。

## 使用规则

规范文档如果使用这些关键词，SHOULD 在文档前部说明关键词语义来自 RFC 2119，或链接到本文件。

`MUST` 和 `MUST NOT` 只能用于真正不可破坏的约束。

适合使用强约束的情况：

- 安全边界。
- 文件职责边界。
- 可被脚本或 reviewer 检查的格式。
- 违反后会污染长期上下文的行为。
- 违反后会让后续 agent 难以恢复的行为。

`SHOULD` 和 `SHOULD NOT` 用于默认策略。

它们表达的是强偏好，不是绝对禁止。agent 可以偏离，但需要说明为什么当前上下文值得偏离。

`MAY` 用于开放空间。

它表示 agent 可以这么做，但不应把它理解成任务要求。

## 强约束使用边界

强约束越多，agent 越难判断真正重要的边界。

写规范时 SHOULD 把 `MUST` 留给会破坏系统、污染长期上下文、导致结构不可解析、或违背用户明确偏好的行为。

如果只是风格偏好、常规建议、可替代方案，SHOULD 使用 `SHOULD` 或 `MAY`。

## 示例

```text
MUST: Markdown 文档必须使用 audience、authors、reviewed_by、purpose、updated。
MUST NOT: 不要把旧偏好保留在 profile 中。
SHOULD: 新增长期维护文档时，应同步更新同层 index.md。
SHOULD NOT: 不应为了当前内容少就合并未来需要独立维护的文档。
MAY: agent 可以在最终回复里建议后续整理方向。
```

## 参考

- RFC 2119: <https://datatracker.ietf.org/doc/html/rfc2119>
- OpenAI Symphony SPEC: <https://github.com/openai/symphony/blob/main/SPEC.md>
