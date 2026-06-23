# Canon Harness

## Audience

This file is for agents performing maintenance work in canon. It defines the read order, workflows, promotion criteria, schemas, and conflict rules.

## Read Order

Before editing canon:

1. Read `CONTEXT.md`.
2. Read this file.
3. Read the relevant subsystem `index.md`.
4. If changing repository architecture, read relevant files in `docs/adr/`.
5. If working in `fragments/`, read `fragments/rules.md` and recent `fragments/log.md` entries.
6. If working in `wiki/`, read `wiki/index.md`, the relevant category `index.md`, and `wiki/log.md`.
7. If working in `profile/`, read `profile/index.md` and the target profile page.

If instructions conflict, stop and surface the conflict. Do not silently override `CONTEXT.md`, `HARNESS.md`, or an accepted ADR.

## Document Rule

Every document must have one audience and one job.

Default to Simplified Chinese for main content because the primary user is a Chinese reader. Keep key technical terms and common English words when they are clearer than forced translation. When introducing an unfamiliar English term, write it as `term(翻译)` the first time; later mentions can use the English term directly.

Do not merge:

- System meaning with operating rules.
- Raw source material with digested source notes.
- Fragment review state with wiki provenance.
- Current profile with deprecated history.
- Canon repository architecture decisions with software engineering theory.

## Root Files

- `AGENTS.md`: route only. It should import the relevant rule files and avoid carrying substantial policy itself.
- `CONTEXT.md`: repository meaning, audience, vocabulary, and boundaries.
- `HARNESS.md`: operating rules for agents.
- `index.md`: layer navigation only.

## Index Architecture

Use split indexes from the start.

Rules:

- Each `index.md` lists only its next layer.
- Root `index.md` links the peer systems.
- A subsystem `index.md` links its direct child directories and key local files.
- A category `index.md` lists pages in that category only.
- Do not create one global page list that crosses multiple layers.

## Fragments Workflow

`fragments/` is the authoritative fragment judgment system.

Fragment lifecycle:

```text
inbox -> review -> verdict -> archive/log
```

Fragments are not long-term assets. Once judged, they disappear from active flow. Wiki pages must not keep backlinks to fragments.

After each review, remove judged fragments from active inbox/review files. Preserve the judged fragment body in `fragments/archive/` only when audit value remains; otherwise the batch log is enough.

Default cadence:

- Weekly distill: judge recent inbox fragments.
- Monthly synthesis and lint: review wiki health and update synthesis where needed.

Allowed verdicts:

- `promote-to-wiki`: the fragment becomes or revises a wiki asset.
- `update-profile`: the fragment updates the current user/context model.
- `preserve-raw`: the fragment points to source material that should be captured under `raw/`.
- `hold-once`: defer exactly once for later review.
- `archive`: keep for audit, but do not promote.
- `discard`: remove from active consideration.

`hold-once` cannot repeat. On the next review, choose a final verdict.

Promotion requires theoretical work. A fragment can enter the wiki only if it does at least one of these:

- `explain`: clarifies a concept.
- `question`: produces a durable question.
- `support`: strengthens a claim.
- `challenge`: weakens or complicates a claim.
- `generalize`: becomes a reusable pattern.
- `revise`: changes synthesis.

## Fragments Logging

`fragments/log.md` records batch-level judgment history, not every fragment body.

Each entry should include:

- Date and review batch.
- Input files.
- Verdict counts.
- Output files.
- Short notes on emerging themes.

The fragment archive and log are audit material. They are not theory sources.

## Raw Workflow

`raw/` stores preserved source material by medium:

- `articles/`
- `papers/`
- `repos/`
- `docs/`
- `videos/`
- `books/`
- `assets/`

Raw files should preserve source fidelity. Do not interpret the material in raw files except for minimal capture metadata needed to identify the source.

Use links only when preserving raw material is impractical.

## Wiki Workflow

`wiki/` stores digested theory assets.

Main categories:

- `sources/`: source notes that digest raw material.
- `concepts/`: stable objects of understanding.
- `claims/`: contestable judgments.
- `patterns/`: reusable structures or practices.
- `examples/`: concrete instances.
- `synthesis/`: higher-level current understanding.
- `questions/`: durable open questions.

Do not copy full raw content into `wiki/sources/`. A source note explains what the source contributes to the theory system.

Reference direction:

```text
raw/<medium>/<source>
  -> wiki/sources/<source-note>
  -> wiki/concepts | wiki/claims | wiki/patterns | wiki/examples | wiki/synthesis | wiki/questions
```

Theory pages should link to `wiki/sources/`, not directly to `raw/`, unless the user explicitly asks for direct evidence inspection.

## Wiki Frontmatter

Use this schema for wiki asset pages. This excludes `index.md` and `log.md` files.

```yaml
---
type: source | concept | claim | pattern | example | synthesis | question
status: draft | active | challenged | retired
confidence: low | medium | high
sources: []
updated: YYYY-MM-DD
---
```

For `wiki/sources/` pages, add `raw`:

```yaml
raw:
  - ../../raw/articles/example.md
```

Do not use `unknown`, `maybe`, `pending`, or `todo` as lifecycle values.

## Wiki Maintenance

When ingesting a source:

1. Preserve or locate the raw material.
2. Update the relevant `raw/<medium>/index.md`.
3. Create or update a `wiki/sources/` source note.
4. Update relevant concepts, claims, patterns, examples, synthesis, or questions.
5. Update the relevant category indexes.
6. Append a batch-level entry to `wiki/log.md`.

When answering a question from the wiki:

1. Read `wiki/index.md`.
2. Drill into relevant category indexes.
3. Read relevant pages.
4. Answer from digested theory with links to wiki pages.
5. If the answer creates durable understanding, ask whether to file it back into the wiki unless the user already requested filing.

When linting the wiki, check for:

- Orphan pages.
- Missing source notes.
- Claims with stale or conflicting evidence.
- Concepts without links to claims, patterns, examples, or sources.
- Patterns without examples.
- Questions that can now be promoted, revised, or retired.
- Synthesis that no longer reflects active claims.

## Profile Workflow

`profile/` stores current trusted context for this canon only.

Rules:

- No `profile/log.md`.
- No confidence fields.
- No deprecated section.
- No inferred/confirmed split.
- Use `updated` because newer profile content usually wins in conflicts.
- If a profile entry becomes wrong, update or remove it.
- Do not assume profile preferences apply to other repositories.
- If a preference looks portable, record it in `profile/portable-candidates.md`; do not export it automatically.

Profile updates are semi-active. If the user expresses a stable preference, goal, or collaboration habit, identify it as profile-worthy before updating.

## Git 规范

本仓库使用 Conventional Commits(约定式提交)。提交信息格式：

```text
<type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

规则：

- `type` 和 `scope` 使用英文；`description` 优先使用简体中文。
- 常用 `type`：`docs` 文档内容，`chore` 仓库维护，`feat` 新能力或新结构，`fix` 修正规则或内容错误，`refactor` 调整组织但不改变语义。
- `scope` 使用被影响的系统或文件职责，例如 `harness`、`context`、`fragments`、`raw`、`wiki`、`profile`、`adr`。
- breaking change(破坏性变更) 使用 `!` 或 footer 中的 `BREAKING CHANGE:` 标记。
- 一个 commit 只表达一个主要意图；如果一个变更同时符合多个 type，优先拆成多个 commit。

示例：

```text
docs(harness): 增加 git 提交规范
fix(profile): 修正用户语言偏好
feat(fragments): 增加 weekly distill 流程
docs(context)!: 调整 canon 上下文边界

BREAKING CHANGE: 不再把 fragments 视为 wiki provenance。
```

## ADR Workflow

`docs/adr/` records architecture decisions for this repository only.

Use ADRs for decisions that shape canon's maintenance behavior, structure, or agent feedback loops.

Do not use ADRs for:

- General software engineering theory.
- Daily notes.
- Fragment content.
- Raw source interpretation.
- Project tasks.

If a proposed repository change contradicts an ADR, surface the contradiction and ask before proceeding.
