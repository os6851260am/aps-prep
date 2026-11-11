# APS Interview Drafts

This directory contains oral course preparation drafts for the **APS (Akademische Prüfstelle) interview**.

Each draft summarizes an undergraduate engineering course into spoken English, structured specifically to answer standard German interview questions:
1. **Overview & Motivation**: Position in the engineering knowledge hierarchy, key focus.
2. **Theory / Core Principles**: 3-5 core concepts, comparisons/trade-offs (e.g., A vs B), and drawing prompts.
3. **Laboratory / Practical Tasks**: Concrete software/hardware tools, step-by-step procedures, and observable results.

---

## Skill Integration (`aps-draft`)

A dedicated Antigravity skill has been configured for this directory:
- **System Path**: `.agents/skills/aps-draft/` (Automatically recognized by Antigravity)
- **Local Shortcut**: [`aps-draft/`](./aps-draft/) (Symlinked directly inside `drafts/`)

### How to Use the Skill
When interacting with the agent, you can simply ask:
- *"帮我写一下 front_end 的草稿"* (Can reference `notes/front_end.md` if available, or automatically reconstruct standard university curriculum and labs).
- *"根据 notes/ 中的笔记生成下一个课程 draft"*
- *"检查并润色 drafts/computer_networks.md 中的口语表达和实验部分"*
