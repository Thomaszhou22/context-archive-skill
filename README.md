<div align="center">

# Context Archive

### Take control of your AI conversation context

[English](#english) | [中文](./README_CN.md)

</div>

---

## English

A skill for [OpenClaw](https://github.com/openclaw/openclaw) that lets users actively manage conversation lifecycle: **archive → free context → recall on demand**.

### The Problem

If you use a single agent session for everything, your context window fills up. Old topics pollute new conversations. The agent loses focus. Tokens get wasted on irrelevant history.

### The Solution

Context Archive gives you three simple actions:

| Action | What it does |
|--------|-------------|
| **Archive** | Summarizes a chunk of conversation into a named `.md` file |
| **List** | Shows all archives with titles, dates, and summaries |
| **Recall** | Loads an archive back into the current context |

### Usage

```
You: 归档最近关于激光投影的讨论
AI: [generates summary] 以上是摘要。有没有遗漏的重要细节？
You: 补充一下，IMU漂移的解决方案那部分要保留
AI: 已更新。标题建议：2026-07-31-激光投影方案。确认？
You: 确认
AI: 已归档至 archives/2026-07-31-激光投影方案.md

--- later ---

You: 有哪些存档
AI: 1. 2026-07-31-激光投影方案 → 激光追踪显示方案对比
    2. 2026-07-15-GitHub统计 → 仓库星数和流量分析

You: 加载第一个
AI: 已加载归档：激光投影方案。关键信息已恢复。
```

### Archive Triggers

- **Topic-based**: "归档关于XX的讨论"
- **Relative time**: "归档最近2小时的对话"
- **Absolute time**: "归档7/21下午3点到5点的对话"
- **Entire day**: "归档今天的对话"
- **Recent (default)**: "归档最近的对话"

### Detail Check

After generating a summary, the agent asks if any important details were missed. You can point to specific conversation segments and the agent will incorporate them. This runs up to two rounds to ensure nothing critical is lost.

### Installation

```bash
clawhub install Thomaszhou22/context-archive-skill
```

Or manually copy `SKILL.md` into your OpenClaw skills directory.

### Archive File Format

Each archive is a structured Markdown file:

```markdown
# Title

> Archived: 2026-07-31 23:49
> Period: 23:00 — 23:49
> Messages: 15

## Summary
{narrative summary}

## Key Points
- {important facts}

## User-Supplied Details
- {details flagged by user during detail check}

## Decisions
- {choices made}

## Files Modified
- path/to/file: what changed

## Keywords
tag1, tag2, tag3
```

### Requirements

- [OpenClaw](https://github.com/openclaw/openclaw) v2.0+
- Write access to workspace `archives/` directory

### Tech Stack

- No dependencies. Pure skill definition.
- Works with OpenClaw's built-in `memory_search`, `read`, and `write` tools.

### License

MIT
