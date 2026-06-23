---
audience: agent
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录 fragments 作为权威碎片裁决系统的决策。
updated: 2026-06-24
status: accepted
---

# ADR-0003: Fragments 作为权威裁决系统

## 背景

用户需要低摩擦捕获想法、观察、链接和非结构化输入。Wiki MUST 保持高密度和理论化，MUST NOT 变成第二个 inbox。

## 决策

`fragments/` 是未裁决输入和裁决的权威系统。

Fragments 会被裁决、记录，并在有 audit 价值时归档，然后从活跃流程中移除。Wiki pages MUST NOT 保留 fragment backlinks。

## 后果

Wiki 保存被提升后的理论资产，不保存 fragment provenance。

Fragment archive 和 log 支持 audit，但它们不是理论来源。
