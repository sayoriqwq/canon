---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义维护 canon 时必须遵守的读取顺序、工作流、schema 和冲突处理规则。
updated: 2026-06-24
---

# Canon 操作守则

## 读取顺序

编辑 canon 前：

1. 读取 `CONTEXT.md`。
2. 读取本文件。
3. 读取相关子系统的 `index.md`。
4. 如果要修改仓库架构，读取 `docs/adr/` 中相关 ADR。
5. 如果要处理 `fragments/`，读取 `fragments/rules.md` 和 `fragments/log.md` 的最近记录。
6. 如果要处理 `wiki/`，读取 `wiki/index.md`、相关 category 的 `index.md` 和 `wiki/log.md`。
7. 如果要处理 `profile/`，读取 `profile/index.md` 和目标 profile 页面。
8. 如果要处理 `vocabulary/`，读取 `vocabulary/index.md` 和目标 vocabulary area。

如果指令冲突，MUST 停止并说明冲突。MUST NOT 静默覆盖 `CONTEXT.md`、`HARNESS.md` 或已接受的 ADR。

## 文档规则

每份 Markdown 文档都是模块，`HARNESS.md` 也不例外。

文档由 metadata 和结构化正文组成。Metadata 是模块头，结构化正文是模块体。

每份文档 MUST 有明确受众和单一职责。

默认使用简体中文作为主内容，因为主要读者是中文读者。关键技术术语和常见英文词在比强行翻译更清楚时 MAY 保留。默认 MUST NOT 给英文术语添加括号中文标注。

Markdown 文档 MUST 用 frontmatter metadata 维护文档读者、来源和用途。MUST NOT 在正文段落里重复写受众。

MUST NOT 创建单独的 `受众` 或 `Audience` 区块；受众信息属于 metadata。

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

MUST NOT 混合：

- 系统意义和操作规则。
- raw 原始材料和消化后的 source note。
- fragment review 状态和 wiki provenance。
- 当前 profile 和过期历史。
- canon 仓库架构决策和软件工程理论。
- 分层 vocabulary 和实现 spec 或临时笔记。

## 根文件

- `AGENTS.md`：只做 route。它 SHOULD 引入相关规则文件，避免承载大量 policy。
- `CONTEXT.md`：仓库意义、读者模型、核心 vocabulary 和边界。
- `HARNESS.md`：agent 操作规则。
- `index.md`：只做层级导航。

## 索引架构

从一开始就使用拆分后的 index。

规则：

- 每个 `index.md` 只列出下一层。
- 根 `index.md` 链接并列系统。
- 子系统 `index.md` 链接它的直接子目录和关键本地文件。
- category `index.md` 只列出该 category 下的页面。
- MUST NOT 创建跨越多个层级的全局页面列表。

## 术语表工作流

`vocabulary/` 保存 canon 中共享的分层术语。

`vocabulary/` 是术语定义的权威位置。`CONTEXT.md` 只路由到它，不保留重复的小型 glossary。

按术语服务的系统边界拆分 vocabulary，不按抽象程度拆分。

- `vocabulary/canon/`：canon 仓库和知识系统术语。
- `vocabulary/agent/`：agent 协作、指令和模型输入输出约束术语。
- `vocabulary/profile/`：用户 profile 和偏好维护术语。

只有出现真实术语群时，MAY 新增 vocabulary area。MUST NOT 创建空的未来区域。

词条格式：

```md
`term`
: 一到两句话定义它是什么。
_Avoid_: 容易混淆的同义词或过载词
```

`_Avoid_` 是可选字段。只有需要拒绝某个混淆同义词或过载词时 MAY 使用。

定义 SHOULD 描述概念边界，MUST NOT 写实现细节或维护流程。

第一轮核心 vocabulary 稳定前，MUST NOT 把 `vocabulary/` 加入 `AGENTS.md`。

## 碎片工作流

`fragments/` 是权威碎片裁决系统。

MUST 使用按月份拆分的 fragment inbox 文件，MUST NOT 使用一个长期滚动的大 inbox 文件。

Fragment 生命周期：

```text
inbox -> review -> verdict -> archive/log
```

Fragments 不是长期资产。裁决后，它们会从活跃流程中消亡。Wiki 页面 MUST NOT 保留指向 fragments 的 backlinks。

每次 review 后，MUST 从活跃 inbox/review 文件中移除已裁决 fragments。只有在仍有审计价值时，MAY 把已裁决 fragment 正文保存在 `fragments/archive/`；否则 batch log 足够。

默认节奏：

- Weekly distill：裁决最近的 inbox fragments。
- Monthly synthesis and lint：检查 wiki 健康度，并按需更新 synthesis。

允许的 verdict：

- `promote-to-wiki`：fragment 成为或修订 wiki asset。
- `update-profile`：fragment 更新当前用户或上下文模型。
- `preserve-raw`：fragment 指向 SHOULD 捕获到 `raw/` 的原始材料。
- `hold-once`：只推迟一次，后续再审。
- `archive`：保留用于 audit，但不提升。
- `discard`：从活跃考虑中移除。

`hold-once` MUST NOT 重复。下一次 review MUST 选择最终 verdict。

提升需要理论工作。Fragment 只有至少完成以下一种动作，才可以进入 wiki：

- `explain`：澄清一个 concept。
- `question`：产生一个 durable question。
- `support`：增强一个 claim。
- `challenge`：削弱或复杂化一个 claim。
- `generalize`：成为可复用 pattern。
- `revise`：改变 synthesis。

## 碎片日志

`fragments/log.md` 记录 batch 级裁决历史，不记录每个 fragment 正文。

每条记录应包括：

- 日期和 review batch。
- 输入文件。
- verdict 数量。
- 输出文件。
- 关于新出现主题的简短 notes。

Fragment archive 和 log 是审计材料。它们不是理论来源。

## 原始材料工作流

`raw/` 按材料形态保存原始材料：

- `articles/`
- `papers/`
- `repos/`
- `docs/`
- `videos/`
- `books/`
- `assets/`

Raw 文件 SHOULD 保持来源保真。除识别来源所需的最小 capture metadata 外，MUST NOT 解释 raw 原始材料。

Raw 原始材料是受保护材料。Agent MUST NOT 改写、翻译、摘要化或重排 raw 正文。

本次全量清理是一次性例外：agent MAY 只为 raw Markdown 添加 metadata。除此之外，raw 正文仍然受保护。

只有在保存 raw 原始材料不实际时，MAY 使用链接。

MUST NOT 创建 `raw/sources/`；`wiki/sources/` 专门用于保存消化后的 source note。

## Wiki 工作流

`wiki/` 保存消化后的理论资产。

主要分类：

- `sources/`：消化 raw 原始材料的 source notes。
- `concepts/`：稳定理解对象。
- `claims/`：可争议判断。
- `patterns/`：可复用结构或实践。
- `examples/`：具体实例。
- `synthesis/`：更高层的当前理解。
- `questions/`：durable open questions。

MUST NOT 把完整 raw content 复制到 `wiki/sources/`。Source note 只说明该 source 对理论系统的贡献。

引用方向：

```text
raw/<medium>/<source>
  -> wiki/sources/<source-note>
  -> wiki/concepts | wiki/claims | wiki/patterns | wiki/examples | wiki/synthesis | wiki/questions
```

理论页面 SHOULD 链接到 `wiki/sources/`，MUST NOT 直接链接到 `raw/`，除非用户明确要求直接检查 evidence。

## Wiki Metadata

Wiki asset 页面使用这个 schema。`index.md` 和 `log.md` 文件不使用此 schema。

```yaml
---
type: source | concept | claim | pattern | example | synthesis | question
status: draft | active | challenged | retired
confidence: low | medium | high
sources: []
updated: YYYY-MM-DD
---
```

`wiki/sources/` 页面需要额外添加 `raw`：

```yaml
raw:
  - ../../raw/articles/example.md
```

MUST NOT 使用 `unknown`、`maybe`、`pending` 或 `todo` 作为生命周期值。

## Wiki 维护

摄入 source 时：

1. 保存或定位 raw 原始材料。
2. 更新相关 `raw/<medium>/index.md`。
3. 创建或更新 `wiki/sources/` source note。
4. 更新相关 concepts、claims、patterns、examples、synthesis 或 questions。
5. 更新相关 category indexes。
6. 向 `wiki/log.md` 追加 batch 级记录。

从 wiki 回答问题时：

1. 读取 `wiki/index.md`。
2. 进入相关 category indexes。
3. 读取相关 pages。
4. 基于消化后的 theory 回答，并链接到 wiki pages。
5. 如果回答产生了 durable understanding，询问是否要写回 wiki，除非用户已经要求写回。

Lint wiki 时，检查：

- 孤立页面。
- 缺失 source notes。
- Claims 有过期或冲突 evidence。
- Concepts 没有链接到 claims、patterns、examples 或 sources。
- Patterns 没有 examples。
- Questions 已经可以 promote、revise 或 retire。
- Synthesis 和 active claims 不一致。

## Profile 工作流

`profile/` 保存跨目录仍然有效的当前可信用户上下文和偏好。Canon 专属操作规则属于 `HARNESS.md`，不属于 `profile/`。

规则：

- MUST NOT 创建 `profile/log.md`。
- MUST NOT 使用 confidence 字段。
- MUST NOT 保留 deprecated 区域。
- MUST NOT 拆分 inferred/confirmed 区域。
- 使用 `updated`，因为发生冲突时，更新的 profile 内容通常优先。
- 如果某条 profile 内容变错了，MUST 直接更新或删除。
- MUST NOT 把 canon-only 的结构、工作流或目录规则写进 `profile/`。
- 如果某条规则只适用于本仓库，MUST 放进 `HARNESS.md` 或 `docs/adr/`。

Profile 更新采用半主动模式。如果用户表达了稳定偏好、目标或协作习惯，更新前 SHOULD 先说明它值得进入 profile。

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
- `scope` MUST 使用被影响的系统或文件职责，例如 `harness`、`context`、`fragments`、`raw`、`wiki`、`profile`、`adr`。
- breaking change MUST 使用 `!` 或 footer 中的 `BREAKING CHANGE:` 标记。
- 一个 commit SHOULD 只表达一个主要意图；如果一个变更同时符合多个 type，SHOULD 优先拆成多个 commit。

示例：

```text
docs(harness): 增加 git 提交规范
fix(profile): 修正用户语言偏好
feat(fragments): 增加 weekly distill 流程
docs(context)!: 调整 canon 上下文边界

BREAKING CHANGE: 不再把 fragments 视为 wiki provenance。
```

## ADR 工作流

`docs/adr/` 只记录本仓库的架构决策。

ADR 用于记录会影响 canon 维护行为、结构或 agent feedback loop 的决策。

MUST NOT 把 ADR 用于：

- 通用软件工程理论。
- 日常笔记。
- Fragment content。
- Raw source interpretation。
- 项目任务。

如果拟议的仓库变更和某个 ADR 冲突，说明冲突并询问后再继续。
