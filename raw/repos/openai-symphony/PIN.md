---
audience: agent
authors:
  - codex
reviewed_by: []
purpose: 作为 openai/symphony raw source 的 pin 锚点，帮助 agent 判断本地 SPEC.md 的来源和更新方式。
updated: 2026-06-24
---

# OpenAI Symphony Pin 锚点

这不是完整 vendor pin，也不是 locator 设计。它只是 `raw/` 中这份源材料的 pin anchor。

## 来源权威

上游仓库是 source of truth：

- upstream: <https://github.com/openai/symphony>
- pinned_ref: `4cbe3a9699a73b862466c0b157ceca0c1985d6d7`
- upstream_path: `SPEC.md`

本地文件只是 raw projection：

- local_path: `raw/repos/openai-symphony/SPEC.md`
- local_sha256: `87fc4348241e74969238346da3119cff66962760708e7618a8dd0ec8d3db75a0`
- upstream_body_sha256: `fa9d7c252cc72d10afdaf4e46e0d890aae28cf4331dc531c94413bc8ea199452`

## 更新提示

更新这份 raw source 时，选择新的 upstream commit，然后从该 commit 下载 `SPEC.md` 覆盖本地正文，并保留本地 metadata。同步更新本文件的 `pinned_ref`、`local_sha256`、`upstream_body_sha256` 和 `updated`。

MUST NOT 把 `main` 的浮动内容直接视为 pinned source。

## 验证提示

MAY 用 pinned ref 对照本地文件：

```bash
curl -fL https://raw.githubusercontent.com/openai/symphony/4cbe3a9699a73b862466c0b157ceca0c1985d6d7/SPEC.md -o /tmp/openai-symphony-SPEC.md
awk 'BEGIN{fm=0} NR==1 && $0=="---"{fm=1; next} fm==1 && $0=="---"{fm=2; next} fm==2 || fm==0{print}' raw/repos/openai-symphony/SPEC.md | tail -n +2 > /tmp/openai-symphony-SPEC-body.md
cmp /tmp/openai-symphony-SPEC.md /tmp/openai-symphony-SPEC-body.md
shasum -a 256 raw/repos/openai-symphony/SPEC.md
```
