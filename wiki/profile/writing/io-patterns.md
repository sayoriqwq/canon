---
audience: agent
authors:
  - codex
reviewed_by: []
purpose: 保存 sayori 对用清晰模式约束模型输入和输出的偏好。
updated: 2026-06-24
---

# 输入输出模式

## 核心判断

面向 agent 的规范应优先使用清晰的模式匹配来约束模型的输入和输出。

描述可以解释意图，但模式决定可执行边界。只写“保持清晰”“注意结构”是不够的；需要给出 agent 可以识别、复用、检查的结构。

## 输入模式

输入模式描述 agent SHOULD 如何读取信息。

常见输入模式包括：

- 文件级 frontmatter。
- 固定字段名。
- 明确的枚举值。
- 明确的目录和文件命名。
- 模板变量和占位符。
- 约定的章节标题。

输入模式的目标是减少 agent 对上下文的猜测，让 agent 能够通过稳定位置和稳定字段快速定位语义。

## 输出模式

输出模式描述 agent SHOULD 如何生成结果。

常见输出模式包括：

- 固定章节顺序。
- 必填字段。
- 允许值列表。
- 状态流转格式。
- 决策记录格式。
- 检查清单格式。

输出模式的目标是让结果可以被人阅读，也可以被后续 agent 或脚本继续处理。

## 一次性和持久化

一次性的模型约束放在 prompt 中。

prompt 适合约束当前任务的输入、输出、语气、步骤和验收条件。它不适合保存长期状态，因为 prompt 会随会话消失。

持久化的模型约束放在文件级结构中，优先使用 frontmatter。

frontmatter 适合保存文档级别的稳定状态，例如 `audience`、`authors`、`reviewed_by`、`purpose`、`updated`。这些信息 SHOULD 可以被 agent 稳定读取，而不是散落在正文描述里。

## 模式优先于描述

当目标是规范 agent 行为时，优先写模式，而不是只写说明。

弱写法：

```text
请注意输出要结构清晰。
```

强写法：

```yaml
result:
  status: accepted | rejected | needs-review
  reason: string
  next_action: string | null
```

前者依赖模型自觉，后者给出可匹配的输出形状。

## 长期维护

如果某个模式会被长期复用，SHOULD 用脚本或检查流程约束它。

prompt 可以建立临时秩序，frontmatter 可以保存持久状态，脚本可以让结构在长期维护中保持稳定。

## 从 Symphony 借鉴

Symphony 的 `WORKFLOW.md` 把文件拆成 frontmatter config 和 prompt body：frontmatter 承载机器可读配置，正文承载交给 agent 的 prompt。

这个设计对 profile 的启发是：

- 持久状态 SHOULD 放进可解析结构，而不是只写在自然语言段落里。
- prompt SHOULD 保持为任务指令，MUST NOT 承担长期配置数据库的职责。
- 模板变量 SHOULD 明确声明；未知变量、未知 filter 这类结构错误 SHOULD 失败，而不是静默降级。
- 文件解析失败、metadata 不是 map、模板渲染失败这类问题 SHOULD 暴露为错误，而不是让 agent 猜。

## 参考

- RFC 2119: <https://datatracker.ietf.org/doc/html/rfc2119>
- OpenAI Symphony: <https://github.com/openai/symphony>
