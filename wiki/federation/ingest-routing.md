---
audience: [agent, human]
authors:
  - codex
reviewed_by:
  - sayori
purpose: 定义 source 或对话成果如何写回 canon wiki federation。
type: pattern
status: active
confidence: medium
sources:
  - ../../llm-wiki.md
updated: 2026-06-25
---

# Ingest Routing

写回必须有 owner。

Ingest 不创建长期 fragment 层。值得保存的内容直接进入 owning sub-wiki；不值得保存的内容留在对话中。

## 流程

```text
source or conversation
  -> identify durable assertion
  -> choose owning sub-wiki
  -> update or create page
  -> update index
  -> add cross-links
  -> append log when useful
```

## 决策

如果内容是原始材料，保存到 `raw/`。

如果内容是当前用户模型或偏好，写入 `wiki/profile/`。

如果内容是共享术语或关系语义，写入 `wiki/vocabulary/`。

如果内容是 canon wiki federation 理论，写入 `wiki/federation/`。

如果内容是软件工程泛化理论，写入 `wiki/software-engineering/`。
