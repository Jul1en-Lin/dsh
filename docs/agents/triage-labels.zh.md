# Triage 标签

[English](triage-labels.md) | 中文

工程 skill（技能）使用五种规范的 triage 角色。本文件把这些角色映射到本仓库使用的标签。

| mattpocock/skills 中的标签 | 本 tracker 中的标签 | 含义                                  |
| -------------------------- | ------------------- | ------------------------------------- |
| `needs-triage`             | `needs-triage`      | 需要维护者评估 Issue                  |
| `needs-info`               | `needs-info`        | 等待报告者补充信息                    |
| `ready-for-agent`          | `ready-for-agent`   | 规格完整，可交给 AFK agent（智能体）  |
| `ready-for-human`          | `ready-for-human`   | 需要由人实现                          |
| `wontfix`                  | `wontfix`           | 不会处理                              |

这些管理用途的标签可与仓库现有的 [GitHub 标签分类体系](../../.agents/notes/implemented/process/2026-08-08-unified-github-label-taxonomy.md)并存。

当 skill 提到一种 triage 角色时，使用表中对应的 tracker 标签。以后仓库修改标签名称时，编辑右侧列即可。
