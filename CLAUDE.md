# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code skill** (not a runnable application) that turns Claude into an expert Midjourney prompt engineer. It ships as a `.skill` file built from the `claude-skill-midjourney-prompter/` directory. There are no build steps, dependencies, tests, or linting — the deliverables are Markdown files.

## Repository Structure

```
claude-skill-midjourney-prompter/
├── SKILL.md                      # Core skill definition (frontmatter + instructions)
└── references/
    ├── parameters.md             # Full parameter reference (all flags, ranges, edge cases)
    └── genre-templates.md        # Prompt templates for 9 visual genres
```

- `SKILL.md` is the entry point. Its YAML frontmatter (`name`, `description`) controls when the skill triggers. The body contains the full prompt-engineering knowledge base.
- `references/` files are supplementary — referenced from SKILL.md via relative paths (e.g., "read `references/parameters.md`").

## Key Conventions

- **Midjourney coverage**: V7 (default), V8 Alpha, Niji 7, and V1 Video. V8.1 is expected but not yet released.
- **Prompt philosophy**: Natural language over keyword soup. The skill enforces a strict hierarchy: Subject → Details → Context → Style → Technical → Parameters.
- **Parameter accuracy matters**: ranges, defaults, and version-specific availability must stay precise. Double-check against `references/parameters.md` when editing.
- **No code**: All content is Markdown. Changes are about factual accuracy, prompt quality, and coverage of Midjourney features — not code style or architecture.
