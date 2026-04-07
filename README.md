# 🎨 Midjourney Prompter

A [Claude skill](https://support.anthropic.com/en/articles/11147530-how-do-i-use-skills) for writing state-of-the-art Midjourney prompts and providing expert tips on Midjourney usage.

Covers **V7**, **V8 Alpha**, **Niji 7**, video generation, and all current parameters as of April 2026.

## What it does

When triggered, Claude becomes an expert Midjourney prompt engineer that:

- **Crafts precise prompts** following the proven Subject → Details → Context → Style → Technical → Parameters hierarchy
- **Explains parameter choices** so you learn as you go
- **Suggests variations** and alternative approaches
- **Provides tips** specific to your use case and chosen model version

## When it triggers

The skill activates when you:

- Ask Claude to write a Midjourney prompt
- Mention Midjourney, MJ, or `/imagine`
- Ask about parameters (`--ar`, `--s`, `--v`, `--no`, `--chaos`, `--weird`, `--sref`, `--oref`, etc.)
- Want to convert an idea into an AI image prompt
- Ask about V7/V8/Niji 7 features or differences
- Request prompt improvement or tips
- Describe a visual scene you want generated

## Installation

Download the latest `.skill` file from [Releases](../../releases) and add it to your Claude skills.

## Repo structure

```
claude-skill-midjourney-prompter/
├── SKILL.md                         # Core skill instructions
└── references/
    ├── parameters.md                # Full parameter reference with ranges & edge cases
    └── genre-templates.md           # Ready-to-adapt templates for 9 genres
```

## What's covered

### Prompt Engineering
- Natural language prompting philosophy (V7+ — no more keyword soup)
- The prompt hierarchy and why word order matters
- Quality signal categories: lighting, materials, atmosphere, camera terms, artist references
- Multi-prompts & weights (`::` syntax)
- Negative prompting (`--no` and negative weights)

### Parameters
- All current parameters with ranges, defaults, and practical advice
- V8 Alpha–specific: `--hd`, `--q 4`, `--exp`
- Reference system: `--oref`, `--sref`, `--iw`, `--cref`
- Video parameters: `--motion`, `--raw`, `--bs`

### Model Selection
- V7 vs V8 Alpha vs Niji 7 — when to use which
- V8 Alpha known issues and workarounds
- Niji 6 legacy style presets

### Genre Templates
Prompt templates and examples for: cinematic realism, portrait photography, product photography, fantasy & sci-fi, anime (Niji 7), architecture, abstract & experimental, food photography, landscape.

### Workflow
- Draft Mode iteration
- Seed-based A/B testing
- Permutation syntax
- Cost management
- Common mistakes & fixes

## Sources

Built from official [Midjourney documentation](https://docs.midjourney.com) and vetted community guides, current as of April 2026 (V8 Alpha, V8.1 imminent).

## License

MIT
