---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 记录文档结构会训练未来维护行为的判断。
type: claim
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Document Structure Trains Maintenance

## 判断

文档结构会训练未来维护行为。

如果一个文档系统最终需要拆分、索引和稳定职责，就应尽早采用目标结构，而不是因为当前内容少就合并成一个大页面。

## 支持

后续 agent 会从现有文件边界、标题、索引和字段中推断可接受的维护方式。临时结构会让后续维护继续复制临时状态。

## 连接

- [Document Module](../concepts/document-module.md)
- [Split Index Document Architecture](../patterns/split-index-document-architecture.md)
