# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is **agNovel** — a Chinese web novel production pipeline with a multi-agent orchestration system. The main agent (`agNovel`) coordinates specialized sub-agents to produce web novels from concept to archived chapters.

## Architecture

```
agNovel (root coordinator)
├── nvl-framer    → Framework design (worldview, protagonist, core conflict)
├── nvl-plotter   → Chapter-by-chapter outline planning
├── nvl-writer    → Chapter content creation
├── nvl-checker   → Critical review (max 3 rounds per chapter)
├── nvl-research  → Platform trend analysis
└── nvl-analysis  → Reader data analysis
```

Each sub-agent is a complete agent with its own directory (`framer/`, `plotter/`, `writer/`, `checker/`), containing:
- `AGENTS.md` — operational procedures
- `SOUL.md` — agent identity and core beliefs
- `IDENTITY.md` — name, role, language
- `TOOLS.md` — tool capabilities and usage
- `USER.md` — user information
- `BOOTSTRAP.md` — initialization script
- `HEARTBEAT.md` — heartbeat marker

## Production Pipeline

1. **Phase 1: Framework** → `nvl-framer` produces `{code}-framer.md`
2. **Phase 2: Outline** → `nvl-plotter` produces `{code}-outliner.md`
3. **Phase 3: Chapter cycle** (repeats for each chapter):
   - `nvl-writer` creates chapter content
   - `nvl-checker` reviews (up to 3 rounds)
   - User confirms final content
   - Chapter archived as `{code}-section-{num}.md`

## Workspace Structure

```
{workspace}/
├── novels/              ← Novel project root
│   └── {code}/          ← Individual novel (named by code)
│       ├── {code}-framer.md
│       ├── {code}-outliner.md
│       └── {code}-section-{num}.md
├── research/            ← Trend reports
│   └── nvl-research-{date}-{num}.md
└── analysis/            ← Data analysis reports
    └── nvl-analysis-{date}-{num}.md
```

## Key Constraints (Red Lines)

- Never write files before user confirmation
- Never skip the checker before archiving chapters
- Never exceed 3 checker rounds per chapter (hard limit enforced at round 3)
- Never create project folders before Phase 1 framework is confirmed
- Pass complete sub-agent output to user without summarization

## Memory System

- `MEMORY.md` at root — current project state, user preferences, known issues
- `memory/YYYY-MM-DD.md` — daily session logs (what was written, review rounds, timestamps)
- Per-agent memory in respective directories via `.openclaw/` subdirectories

## Language

All work is conducted in **Simplified Chinese** (中文简体). All documentation, file content, and agent communications use UTF-8 encoding.
