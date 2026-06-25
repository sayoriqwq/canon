---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 描述用拆分索引维护长期文档系统的模式。
type: pattern
status: active
confidence: high
sources:
  - ../sources/profile-writing.md
updated: 2026-06-24
---

# Split Index Document Architecture

## 模式

长期维护的文档系统应使用拆分后的 index：每个 index 只链接下一层，category index 只列出本 category 下的页面。

不要因为当前文件少，就保留未来会变成全局列表的大 index。

## 适用场景

- 文档系统预计持续增长。
- 文档有多个并列子系统或 category。
- agent 需要通过稳定路径定位页面。

## 连接

- [Document Module](../concepts/document-module.md)
- [Document structure trains maintenance](../claims/document-structure-trains-maintenance.md)
