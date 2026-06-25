---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 保存 canon 和 wiki federation 的核心术语。
updated: 2026-06-25
---

# Canon 术语表

## 词条

`personal LLM-wiki federation`
: 以 LLM-wiki 模式维护的个人 wiki 联邦；`wiki/` 是唯一长期知识主体，内部按 sub-wiki ownership 拆分。

`sub-wiki`
: `wiki/` 下的 assertion ownership 区域。Sub-wiki 对用户不是必填入口，对 agent 是写回和维护边界。

`assertion ownership`
: 一条 durable assertion 由一个 sub-wiki 或 raw source 拥有的关系。它用来防止同一内容在多个位置成为真源。

`raw`
: 被保存的原始材料层。Raw 用于来源保真和后续检查，不用于解释。

`source note`
: sub-wiki 中消化 raw 或内部 source 的页面，用来说明该 source 对 owning sub-wiki 理论或模型的贡献。

`wiki asset`
: `wiki/` 下由某个 sub-wiki owning 的 durable 页面，例如 source note、concept、claim、pattern、example、synthesis、question 或 profile page。

`concept`
: 稳定的理解对象，例如 document module、assertion、normative keyword。

`claim`
: 可争议的判断，可以被支持、挑战、修订或退休。

`pattern`
: 可复用的结构或实践，可以指导设计或实现。

`example`
: 用来说明 concept、claim 或 pattern 的具体实例。

`synthesis`
: 由 sources、concepts、claims、patterns、examples、questions 连接后形成的当前高层理解。

`pin anchor`
: raw source 的轻量来源锚点，记录 upstream、pinned ref、本地投影和验证方式。它不是完整 vendor pin，也不替代 upstream authority。
