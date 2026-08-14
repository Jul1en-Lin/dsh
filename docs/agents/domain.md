# Domain docs

English | [中文](domain.zh.md)

These rules tell engineering skills where to find domain terminology and decisions before exploring code.

## Before exploring, read these

- Read the root `CONTEXT-MAP.md`, then each relevant `CONTEXT.md` it names.
- Read active [Agent Notes](../../.agents/notes/README.md) that affect the area being explored.
- Treat archived Agent Notes as historical evidence rather than current instructions.

If a context file does not exist, proceed silently. Do not propose one merely because it is absent. The `/domain-modeling` skill creates context files when terminology is actually resolved.

This repository records system-wide and context-specific decisions as Agent Notes under `.agents/notes/`. A `CONTEXT.md` may link to an Agent Note, but it does not duplicate the decision in a parallel `docs/adr/` tree.

## File structure

`CONTEXT-MAP.md` owns the current list and location of contexts. A context may cover a package group, an application, or a capability spanning several packages.

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

Context files are created only when needed; this setup does not create placeholder contexts.

## Use glossary terminology

When output names a domain concept in an issue, proposal, hypothesis, or test, use the term defined by the relevant `CONTEXT.md`.

If the concept is missing, reconsider whether the term belongs to the project. If the gap is real, record it for `/domain-modeling`.

## Surface decision conflicts

If an output contradicts an active Agent Note, state the conflict explicitly instead of silently overriding it:

> _Contradicts the active Agent Note that owns this decision, but may be worth reopening because…_
