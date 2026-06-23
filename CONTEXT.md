# Canon Context

## Audience

This file is for agents and the future maintainer of this repository. Read it to understand what this repository is, what it is not, and which vocabulary must be preserved when maintaining it.

Every document in this repository must know its audience. Do not write or reshape a document until its reader and use case are clear.

## Purpose

Canon is a personal software engineering theory system.

It serves the user described in `profile/learning-profile.md`: a developer building long-term understanding around modern software systems.

The goal is not to collect notes. The goal is to compile learning inputs into durable engineering judgment.

## Non-Goals

Canon is not:

- A project task tracker.
- A prompt snippet dump.
- A repository-specific coding rule collection.
- A generic technology taxonomy.
- A place to store every interesting fragment forever.
- A replacement for the concrete repositories where practice happens.

Practice happens in concrete repositories. Canon stores theory extracted from practice only when it becomes reusable understanding.

## Core Feedback Loop

The system exists to support this loop:

```text
material or fragment
  -> capture
  -> judge
  -> digest
  -> connect
  -> revise current understanding
  -> improve future reading, coding, and agent collaboration
```

If a change does not improve this loop, treat it as suspect.

## System Layers

Canon 是 single-context 仓库，不使用 `CONTEXT-MAP.md`。

仓库有四个并列系统：

- `fragments/`：权威碎片裁决系统。
- `raw/`：按材料形态保存的原始材料。
- `wiki/`：消化后的理论资产。
- `profile/`：跨目录仍然有效的当前用户上下文和偏好。

它们是同一个系统的不同层，不是彼此独立的 domain context。

## Vocabulary

Use these terms consistently.

`fragment`
: An unresolved input such as an idea, observation, question, quote, hunch, or unstructured note. A fragment is judged and then disappears from the active flow.

`raw`
: Preserved source material. Raw files are for fidelity and later inspection, not interpretation.

`source note`
: A page under `wiki/sources/` that digests a raw source and explains its contribution to the theory system.

`concept`
: A stable object of understanding, such as state, boundary, runtime, tool use, memory, or type modeling.

`claim`
: A contestable judgment that may be supported, challenged, revised, or retired.

`pattern`
: A reusable structure or practice that can guide design or implementation.

`example`
: A concrete instance that illustrates a concept, claim, or pattern.

`synthesis`
: The current higher-level understanding produced by connecting sources, concepts, claims, patterns, examples, and questions.

`profile`
: 关于用户、学习目标和协作偏好的当前可信上下文，且这些内容需要跨目录仍然有效。项目专属操作规则不属于这里。

## Audience By Layer

- `CONTEXT.md`: agents and future maintainers who need repository meaning and boundaries.
- `HARNESS.md`: agents actively maintaining canon.
- `docs/adr/`: agents or maintainers changing canon's architecture.
- `fragments/`: agents and the user during capture, review, and distillation.
- `raw/`: agents and the user when source fidelity must be checked.
- `wiki/`: the user learning and thinking, and agents answering from digested theory.
- `profile/`：跨目录协作中的 agent。

## Architectural Principles

- Prefer single-responsibility documents.
- Prefer split index architecture from the start, even when the repository is small.
- Do not keep one large index simply because there are few files.
- Do not let fragments become permanent theory assets.
- Do not put raw source material directly into theory pages.
- Do not keep outdated preferences in `profile/`.
- Do not promote canon repository decisions into `wiki/` unless the user explicitly asks to generalize them into software engineering theory.
