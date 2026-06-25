---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义维护 canon wiki federation 时必须遵守的读取顺序、路由、写回和检查规则。
updated: 2026-06-25
---

# Canon 操作守则

## 读取顺序

编辑 canon 前：

1. 读取 `CONTEXT.md`。
2. 读取本文件。
3. 读取 `wiki/index.md`，理解 federation map。
4. 读取相关 sub-wiki 的 `index.md`。
5. 如果要修改仓库架构，读取 `docs/adr/index.md` 和相关 ADR。
6. 如果要处理 raw 原始材料，读取 `raw/index.md` 和对应材料形态的 `index.md`。
7. 如果要修改 wiki federation 理论，读取 `wiki/federation/index.md`。
8. 如果要处理用户模型和偏好，读取 `wiki/profile/index.md` 和目标页面。
9. 如果要处理术语，读取 `wiki/vocabulary/index.md` 和目标 vocabulary area。
10. 如果要处理软件工程理论，读取 `wiki/software-engineering/index.md`、相关 category 的 `index.md` 和 `wiki/software-engineering/log.md`。

如果指令冲突，MUST 停止并说明冲突。MUST NOT 静默覆盖 `CONTEXT.md`、`HARNESS.md` 或已接受的 ADR。

## 顶层模型

Canon 是 personal LLM-wiki federation。

`wiki/` 是唯一长期知识主体。`wiki/` 内的 sub-wiki 是 assertion ownership 区域。用户不需要指定 sub-wiki；agent MUST 根据问题和写回内容路由。

`raw/` 是原始材料层，不是 wiki。Raw 文件 SHOULD 保持来源保真。除识别来源所需的最小 capture metadata 外，MUST NOT 改写、翻译、摘要化或重排 raw 正文。

`fragments/` 不属于 canon。MUST NOT 恢复根目录 `fragments/`、长期 inbox、review backlog 或 prompt dump。如果一次对话产生值得保存的内容，MUST 直接编译进一个 owning sub-wiki；否则不在 canon 内长期保存。

## 核心不变量

```text
read can be federated
write must be owned
links can cross sub-wiki
assertions cannot have duplicate owners
```

一个回答可以读取多个 sub-wiki。一次写回必须明确 owning sub-wiki。

同一条 durable assertion 只能有一个 owner。其他页面只能链接、引用、摘要、派生、泛化或投影，MUST NOT 复制成第二真源。

Sub-wiki 按 assertion ownership 分，不按主题词分。判断归属时看页面主张是什么：

- 关于 sayori 当前模型、偏好、协作语义：`wiki/profile/`。
- 关于 canon wiki federation 本身：`wiki/federation/`。
- 关于共享术语和关系语义：`wiki/vocabulary/`。
- 关于软件工程、文档维护、agent-facing 文档等泛化理论：`wiki/software-engineering/`。

## 文档规则

每份 Markdown 文档都是模块，`HARNESS.md` 也不例外。

文档由 metadata 和结构化正文组成。Metadata 是模块头，结构化正文是模块体。

每份文档 MUST 有明确受众和单一职责。

默认使用简体中文作为主内容。关键技术术语和常见英文词在比强行翻译更清楚时 MAY 保留。默认 MUST NOT 给英文术语添加括号中文标注。

Markdown 文档 MUST 用 frontmatter metadata 维护文档读者、来源和用途。MUST NOT 在正文段落里重复写受众。

基础 metadata：

```yaml
audience: agent | human | [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 一句话说明这份文档帮助读者完成什么
updated: YYYY-MM-DD
```

规则：

- `audience` 只描述读者类型，不写具体人名、场景或任务。
- `authors` 描述文档由谁生成或主要撰写。
- `reviewed_by` 描述谁明确 review 或批准过该文档。
- `purpose` 描述文档的使用场景。
- 不使用 `owner` 表达生成者或批准者。
- MUST NOT 创建单独的 `受众` 或 `Audience` 区块；受众信息属于 metadata。

MUST NOT 混合：

- 系统意义和操作规则。
- raw 原始材料和 wiki 编译内容。
- 当前用户模型和过期历史。
- schema 规则和 federation 理论。
- 仓库 ADR 和 sub-wiki 理论页面。
- 术语定义和实现 spec 或临时笔记。

## 根文件

- `AGENTS.md`：只做 route。它 SHOULD 引入相关规则文件，避免承载大量 policy。
- `CONTEXT.md`：仓库意义、边界和顶层架构。
- `HARNESS.md`：agent 操作规则。
- `index.md`：仓库入口。
- `llm-wiki.md`：外部原始参照。

## 索引架构

使用 split index architecture。

规则：

- 根 `index.md` 只链接顶层入口。
- `wiki/index.md` 是 federation map，只列 sub-wiki 和 federation-level 文件。
- Sub-wiki `index.md` 只列本 sub-wiki 的直接子目录和关键本地文件。
- Category `index.md` 只列该 category 下的页面。
- MUST NOT 创建跨越多个层级的全局页面列表。

## Query 路由

从 canon 回答问题时：

1. 读取 `wiki/index.md`。
2. 根据问题识别 candidate owning sub-wiki。
3. 读取 candidate sub-wiki 的 `index.md`。
4. 读取相关页面；必要时读取其它 sub-wiki 的相关页面。
5. 回答时说明主要依据的 sub-wiki 边界。
6. 如果回答产生 durable knowledge，写回前先判断 owning sub-wiki。

常见路由：

- “我偏好 agent 怎么做？” -> `wiki/profile/`
- “这个词在 canon 里是什么意思？” -> `wiki/vocabulary/`
- “wiki federation 应该怎么运作？” -> `wiki/federation/`
- “文档维护有哪些可复用理论？” -> `wiki/software-engineering/`

## Ingest 路由

摄入 source 或对话成果时：

1. 确认 evidence：raw source、已有 wiki 页面或当前 conversation。
2. 判断要写入的 durable assertion。
3. 选择一个 owning sub-wiki。
4. 更新 owning 页面或创建新页面。
5. 更新 owning sub-wiki 的 index。
6. 建立必要 cross-links。
7. 追加相关 log；如果 sub-wiki 没有专属 log，追加到最近的 owning log 或说明不需要日志。

MUST NOT 因为一个内容涉及多个主题就复制到多个 sub-wiki。

如果需要从一个 sub-wiki 派生另一个 sub-wiki 的理论，使用链接和 source note，而不是复制原文。

## Sub-wiki 规则

### `wiki/federation/`

保存 canon 自己的 wiki federation 理论。

它可以引用 `llm-wiki.md`，但 MUST NOT 把 `llm-wiki.md` 原文复制进理论页面。

它回答：sub-wiki 是什么、ownership 如何判断、query/ingest/lint 如何跨 sub-wiki 工作、链接如何表达语义、唯一真源如何保持。

### `wiki/profile/`

保存当前有效、跨目录仍然成立的用户模型、偏好和协作语义。

规则：

- MUST NOT 保留 deprecated 偏好。
- MUST NOT 使用 confidence 字段。
- MUST NOT 拆分 inferred/confirmed 区域。
- 使用 `updated` 辅助解决冲突。
- 如果某条 profile 内容变错了，MUST 直接更新或删除。
- MUST NOT 把 canon-only 的结构、工作流或目录规则写进 profile 页面。

### `wiki/vocabulary/`

保存跨 sub-wiki 共享的术语、关系语义和边界。

优先按术语服务的语义边界分层，而不是按抽象程度分层。

如果一个术语主要服务 canon 和 wiki federation，放入 `wiki/vocabulary/canon/`。

如果一个术语主要服务 agent 协作、指令规范、模型输入输出约束，放入 `wiki/vocabulary/agent/`。

如果一个术语主要服务用户模型和偏好维护，放入 `wiki/vocabulary/profile/`。

当某个 sub-wiki 的共享术语规模变大，MAY 新增专门 vocabulary 区域；MUST NOT 提前创建空目录。

词条格式：

```md
`term`
: 一到两句话定义它是什么。
_Avoid_: 容易混淆的同义词或过载词
```

`_Avoid_` 是可选字段。定义 SHOULD 描述概念边界，MUST NOT 写实现细节或维护流程。

### `wiki/software-engineering/`

保存软件工程和 agent-facing 文档相关的理论资产。

Source note 说明 raw source 或明确提升的内部 source 对 software-engineering sub-wiki 的贡献，MUST NOT 复制完整 source 正文。

当前主要 category：

- `sources/`：消化 raw 或内部 source 的 source notes。
- `concepts/`：稳定理解对象。
- `claims/`：可争议判断。
- `patterns/`：可复用结构或实践。
- `examples/`：具体实例。
- `synthesis/`：高层当前理解。
- `questions/`：durable open questions。

## Wiki Metadata

理论 asset 页面可使用这个 schema。`index.md` 和 `log.md` 文件不使用此 schema。

```yaml
---
type: source | concept | claim | pattern | example | synthesis | question
status: draft | active | challenged | retired
confidence: low | medium | high
sources: []
updated: YYYY-MM-DD
---
```

`sources/` 页面可以额外添加 `raw`。该字段记录 source note 消化的源文件；通常是 `raw/` 文件，也可以是用户明确允许作为 source 的内部 wiki 页面：

```yaml
raw:
  - ../../../raw/articles/example.md
```

MUST NOT 使用 `unknown`、`maybe`、`pending` 或 `todo` 作为 lifecycle 值。

## Lint

Lint canon 时，检查：

- 根目录是否重新出现 `profile/`、`vocabulary/` 或 `fragments/`。
- Durable assertions 是否有多个 owners。
- Cross-link 是否指向迁移前旧路径。
- `wiki/index.md` 是否准确列出 sub-wiki。
- Sub-wiki index 是否只列下一层。
- Raw source 是否被改写或解释。
- Theory 页面是否缺少 source note 或 evidence。
- Profile 页面是否保存过期偏好。
- Vocabulary 页面是否混入流程说明或实现 spec。
- Federation 理论和 `HARNESS.md` 是否混合。

## Git 规范

本仓库使用 Conventional Commits。提交信息格式：

```text
<type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

规则：

- `type` 和 `scope` MUST 使用英文；`description` SHOULD 优先使用简体中文。
- 常用 `type`：`docs` 文档内容，`chore` 仓库维护，`feat` 新能力或新结构，`fix` 修正规则或内容错误，`refactor` 调整组织但不改变语义。
- `scope` MUST 使用被影响的系统或文件职责，例如 `harness`、`context`、`wiki`、`raw`、`adr`。
- breaking change MUST 使用 `!` 或 footer 中的 `BREAKING CHANGE:` 标记。
- 一个 commit SHOULD 只表达一个主要意图。

## ADR 工作流

`docs/adr/` 只记录本仓库的架构决策。

ADR 用于记录会影响 canon 维护行为、结构或 agent feedback loop 的决策。

当架构发生明显 breaking change 时，MUST 删除被取代的旧 ADR，而不是保留 superseded ADR 污染模型上下文。新的 ADR 应完整表达当前有效决策和必要后果。

MUST NOT 把 ADR 用于：

- 通用软件工程理论。
- 日常笔记。
- Raw source interpretation。
- 项目任务。

如果拟议的仓库变更和某个 ADR 冲突，说明冲突并询问后再继续。
