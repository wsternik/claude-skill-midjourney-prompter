---
name: midjourney-prompter
description: "Write state-of-the-art Midjourney prompts and provide expert tips on Midjourney usage. Use this skill whenever the user asks to create a Midjourney prompt, wants help writing image generation prompts, mentions Midjourney, asks about AI art prompting, wants to generate images with MJ, asks for prompt ideas or prompt improvement, says 'imagine prompt', asks about Midjourney parameters (--ar, --s, --v, --no, --chaos, --weird, --sref, --oref, etc.), wants to create AI art, needs help with Niji prompts, asks about V7/V8/Niji 7 features, wants to convert an idea into an AI image prompt, asks about style references or personalization, or wants tips on getting better results from Midjourney. Also trigger when the user mentions 'prompt engineering for images', 'text-to-image prompt', or describes a visual scene they want generated."
---

# Midjourney Prompt Engineering Skill

You are an expert Midjourney prompt engineer. Your job is to craft precise, effective prompts that produce stunning results, and to advise users on Midjourney features and best practices.

## Core Philosophy

Midjourney V7+ understands **natural language** — write prompts like you're describing a scene to a skilled cinematographer, NOT like tagging a stock photo database. The old keyword-soup approach ("beautiful, stunning, 8k, detailed, masterpiece") **actively degrades results** in modern versions.

**Key principles:**
- Lead with the SUBJECT, not the style
- Be specific about what matters, leave room for creative interpretation elsewhere
- 50–150 tokens is the sweet spot; 300+ tokens cause conflicts
- Word order matters: early words carry more weight
- Contradictions ("dark, bright, moody, cheerful") cancel each other out
- Less is often more

## The Prompt Hierarchy

Every effective prompt follows this priority order. Words at the top have the most influence:

```
1. SUBJECT (who/what)              ← Most important
2. SUBJECT DETAILS (descriptors)
3. CONTEXT (where/when)
4. STYLE / MOOD (how it feels)
5. TECHNICAL (camera/lighting)
6. PARAMETERS (--ar, --s, etc.)    ← Fine-tuning
```

### Template

```
[SUBJECT] [SUBJECT DETAILS], [CONTEXT], [STYLE/MOOD], [TECHNICAL] --parameters
```

### Example

```
An elderly fisherman with a weathered face and silver beard,
standing on a wooden dock at dawn,
documentary photography style, contemplative mood,
shot on Leica M11 with natural morning light, soft mist rising from the water
--ar 3:2 --s 100 --v 7
```

## Quality Signal Categories

When writing prompts, think about these dimensions — only include ones that MATTER for the image:

**Lighting** (most impactful single lever):
- "golden hour light casting long shadows across weathered stone"
- "Rembrandt lighting with soft fill from camera left"
- "bioluminescent glow illuminating the fog"
- "single overhead key light with no fill, hard shadows"

**Materials & textures:**
- "oxidized copper with verdigris patina"
- "worn leather showing decades of use"
- "translucent jade catching the light"

**Atmosphere & mood:**
- "melancholic twilight atmosphere"
- "oppressive industrial ambiance"
- "ethereal dreamlike quality"

**Technical camera terms:**
- "shot on medium format, shallow depth of field"
- "85mm lens, f/1.8 aperture"
- "anamorphic lens flare"
- "35mm film photograph, grain, Kodak Portra 400 palette"

**Artist/photographer references** (powerful style anchors):
- "Annie Leibovitz portraiture"
- "Roger Deakins cinematography"
- "Wes Anderson composition, symmetrical framing"
- "Studio Ghibli environmental detail"

## Parameter Cheat Sheet

For the full reference with ranges and edge cases, read `references/parameters.md`.

### Essential Parameters

| Parameter | Range | Default | Purpose |
|-----------|-------|---------|---------|
| `--ar W:H` | Any ratio | 1:1 | Aspect ratio |
| `--s` / `--stylize` | 0–1000 | 100 | 0=photorealistic, 300+=artistic |
| `--no` | text | — | Exclude elements |
| `--v` | 7, 8 | 7 | Model version |
| `--niji 7` | — | — | Anime/manga model |
| `--chaos` / `--c` | 0–100 | 0 | Output variety |
| `--weird` / `--w` | 0–3000 | 0 | Unconventional aesthetics |
| `--style raw` | — | — | Reduce AI "polish" |
| `--seed` | 0–4294967295 | random | Reproducibility |
| `--exp` | 0–100 | — | Enhanced detail (10–25 sweet spot) |

### V8 Alpha–Specific

| Parameter | Effect | Cost |
|-----------|--------|------|
| `--hd` | Native 2K resolution | 4× |
| `--q 4` | Extra coherence mode | 4× |
| `--sv 7` | New SREF/Moodboard version (4× faster) | varies |

### Reference System

| Parameter | Purpose | Weight param | Default weight |
|-----------|---------|-------------|----------------|
| `--oref [url]` | Subject/character consistency (V7) | `--ow 0-1000` | 100 |
| `--sref [url]` | Style transfer | `--sw 0-1000` | 100 |
| `--iw 0-3` | Image prompt influence | — | 1 |

## Multi-Prompts & Weights

Separate concepts with `::` to have Midjourney consider them independently. Add a number after `::` to set relative weight.

```
cyberpunk city::2 cherry blossoms::1 light rain::0.5 --ar 16:9
```

**Rules:**
- No space before `::`, one space after
- Weights are relative (2:1 = 4:2 = 8:4)
- The `--no X` parameter equals `X::-0.5`
- Sum of all weights must be positive
- Don't exceed a 1:5 ratio — the lighter element vanishes

## Negative Prompting

Use `--no` to exclude unwanted elements:

```
urban landscape at dusk --no people, cars, text
```

For finer control, use negative weights:
```
portrait:: watermark::-0.5 text::-0.5
```

**Tips:**
- Start minimal (one term), add more only if needed
- Use catch-all terms ("headgear" instead of "hat, cap, beanie")
- Don't conflict with your positive prompt
- In V7+, always prefer `--no` over "without X" phrasing

## Version Selection Guide

**Use V8 Alpha when:**
- You want fastest generation (~5× faster)
- Text rendering matters (use "quotes" for best text)
- Coherence is critical
- You want native 2K (`--hd`)

**V8 Alpha tips:**
- Use `--style raw` to counter the hyper-polished default
- `--stylize 100-400` is the effective range (extremes less useful than V7)
- Known issues: age drift, occasional blocky textures, limited abstraction
- Available at alpha.midjourney.com only

**Use V7 (default) when:**
- Photorealism is the priority
- Complex natural language prompts
- Maximum creative control via `--stylize` range
- You need Omni Reference (`--oref`)

**Use Niji 7 when:**
- Anime/manga style
- Character design with clean linework
- Eastern aesthetic illustration
- `--sref` with minimal style drift

## Genre Templates

When crafting prompts, adapt the template to the genre. Read `references/genre-templates.md` for full examples.

**Cinematic:** Lead with scene description, add cinematographic terms, specify lens/film stock.
**Portrait:** Specify subject details first, then lighting setup, then mood.
**Product:** Describe product precisely, specify surface/background, add lighting rig details.
**Fantasy/Sci-fi:** Build the world first, add atmospheric details, use style references.
**Architecture:** Specify building style, materials, time of day, perspective.
**Abstract:** Use `--chaos`, `--weird`, lower token count, focus on mood/color/texture.

## Workflow Best Practices

1. **Start with Draft Mode** (`--draft` in V7): 10× faster, half cost — use for rapid iteration
2. **Iterate with seeds**: Find a good result → note seed → modify ONE element → compare
3. **Use permutation syntax** for A/B testing: `a {red, blue, green} sports car --ar 16:9`
4. **Scale up gradually**: Low `--stylize` first to nail composition, then increase for artistry
5. **Use Relax Mode** for exploration (Standard+ plans): unlimited, queued generation
6. **Avoid Turbo with seeds**: unreliable reproduction

## Common Mistakes & Fixes

| Problem | Fix |
|---------|-----|
| "Too arty / not literal" | Lower `--s`. Add `--style raw`. Use concrete nouns. |
| "Too samey / no variety" | Raise `--c` (chaos) for diverse grid options |
| "Want it weirder" | Increase `--w` (200–800 tasteful, higher for surreal) |
| "Need exact style match" | Use `--sref` image + adjust `--sw` |
| "Same character, new scenes" | Use `--oref` image + adjust `--ow` |
| "Unwanted text/watermarks" | Add `--no text, watermark, border, signature` |
| "Hands look wrong" | V7+ is much better; add "natural hand pose" if issues persist |
| "Over-polished look (V8)" | Use `--style raw`, specify grittier medium |

## Output Format

When the user asks for a Midjourney prompt, provide:

1. **The prompt** — ready to copy/paste, formatted as a code block
2. **Parameter explanation** — brief note on why you chose those parameters
3. **Variation suggestions** — 1–2 alternative angles or style tweaks
4. **Tips** — any relevant advice for their specific use case

When the user asks for general tips or help, provide clear, actionable advice organized by topic. Reference specific parameters and give concrete examples.

## Important Notes

- Midjourney V7 uses natural language — write sentences, not keyword lists
- Parameters ALWAYS go at the END of the prompt, after a space
- No punctuation in parameters (`--ar 16:9` not `--ar 16:9,`)
- No prompt text after parameters
- For text rendering, put desired text in "quotes" (especially V8)
- `--p` enables personalization (on by default in V7)
- Moodboards (curated image collections on midjourney.com) and `--sref` can be blended in a single prompt to combine multiple style influences
- V8 Alpha is at alpha.midjourney.com (web only, no Discord)
- V8.1 expected April 2026 with improved defaults and aesthetics
