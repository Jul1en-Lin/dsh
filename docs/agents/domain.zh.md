# 领域文档

[English](domain.md) | 中文

这些规则说明工程 skill 在探索代码前应到哪里查找领域术语和决策。

## 探索前读取这些内容

- 读取根目录的 `CONTEXT-MAP.md`，再读取其中列出的每个相关 `CONTEXT.md`。
- 读取会影响当前领域的活跃 [Agent Notes](../../.agents/notes/README.md)。
- 归档 Agent Note 只作为历史依据，不作为当前指令。

如果上下文文件不存在，直接继续。不要仅因为文件缺失就提议创建。`/domain-modeling` skill 会在术语真正确定时创建上下文文件。

本仓库将系统级和上下文级决策记录为 `.agents/notes/` 下的 Agent Notes。`CONTEXT.md` 可以链接到 Agent Note，但不会把决策复制到另一套 `docs/adr/` 目录中。

## 文件结构

`CONTEXT-MAP.md` 记录当前上下文清单及其位置。一个上下文可以覆盖一个包组、一个应用，或横跨多个包的能力。

```text
/
├── CONTEXT-MAP.md
├── .agents/
│   └── notes/
└── packages/
    ├── session/
    │   └── CONTEXT.md
    └── workflow/
        └── CONTEXT.md
```

上下文文件只在需要时创建；本次设置不会创建占位上下文。

## 使用术语表中的用词

当输出在 Issue、提案、假设或测试中提到领域概念时，使用相关 `CONTEXT.md` 定义的术语。

如果概念缺失，先重新判断这个词是否属于项目。如果确实存在缺口，把它记录给 `/domain-modeling`。

## 明确指出决策冲突

如果输出与活跃 Agent Note 冲突，应明确说明，而不是静默覆盖：

> _与记录该决策的活跃 Agent Note 冲突，但可能值得重新讨论，因为……_
