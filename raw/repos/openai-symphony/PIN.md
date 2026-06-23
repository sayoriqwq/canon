---
audience: agent
authors:
  - codex
reviewed_by: []
purpose: 作为 openai/symphony raw source 的 pin 锚点，帮助 agent 判断本地 SPEC.md 的来源和更新方式。
updated: 2026-06-23
---

# OpenAI Symphony Pin

这不是完整 vendor pin，也不是 locator 设计。它只是 `raw/` 中这份源材料的 pin anchor。

## Source Authority

上游仓库是 source of truth：

- upstream: <https://github.com/openai/symphony>
- pinned_ref: `4cbe3a9699a73b862466c0b157ceca0c1985d6d7`
- upstream_path: `SPEC.md`

本地文件只是 raw projection：

- local_path: `raw/repos/openai-symphony/SPEC.md`
- sha256: `fa9d7c252cc72d10afdaf4e46e0d890aae28cf4331dc531c94413bc8ea199452`

## Update Hint

更新这份 raw source 时，选择新的 upstream commit，然后从该 commit 下载 `SPEC.md` 覆盖本地文件，并同步更新本文件的 `pinned_ref`、`sha256` 和 `updated`。

不要把 `main` 的浮动内容直接视为 pinned source。

## Verify Hint

可以用 pinned ref 对照本地文件：

```bash
curl -fL https://raw.githubusercontent.com/openai/symphony/4cbe3a9699a73b862466c0b157ceca0c1985d6d7/SPEC.md -o /tmp/openai-symphony-SPEC.md
cmp /tmp/openai-symphony-SPEC.md raw/repos/openai-symphony/SPEC.md
shasum -a 256 raw/repos/openai-symphony/SPEC.md
```
