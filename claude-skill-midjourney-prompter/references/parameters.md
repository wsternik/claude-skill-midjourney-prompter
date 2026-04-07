# Midjourney Parameters Reference

## Table of Contents
1. [Aspect Ratio](#aspect-ratio)
2. [Stylize](#stylize)
3. [Chaos](#chaos)
4. [Weird](#weird)
5. [Experimental](#experimental)
6. [Quality](#quality)
7. [Seed](#seed)
8. [No (Negative)](#no-negative)
9. [Style Raw](#style-raw)
10. [Stop](#stop)
11. [Tile](#tile)
12. [Repeat](#repeat)
13. [Draft Mode](#draft-mode)
14. [Personalization](#personalization)
15. [Moodboards](#moodboards)
16. [Image Weight](#image-weight)
17. [Version & Model](#version-model)
18. [V8-Specific](#v8-specific)
19. [Reference System](#reference-system)
20. [Video Parameters](#video-parameters)

---

## Aspect Ratio
`--ar W:H` or `--aspect W:H`

Default: 1:1 (square)

### Platform Recommendations
| Platform | Ratio |
|----------|-------|
| Instagram Feed | `1:1` or `4:5` |
| Instagram Story / TikTok | `9:16` |
| YouTube Thumbnail | `16:9` |
| Twitter/X | `16:9` |
| Pinterest | `2:3` |
| Desktop wallpaper | `16:9` or `21:9` |
| Phone wallpaper | `6:11` or `9:16` |
| Cinematic | `21:9` |
| Photo print | `3:2` or `2:3` |

### Composition Impact
- Wide (16:9, 21:9): emphasizes environment, natural for landscapes and cinematic scenes
- Tall (2:3, 9:16): emphasizes subject height, good for portraits and vertical content
- Square (1:1): balanced, centers the subject

---

## Stylize
`--s VALUE` or `--stylize VALUE`

Range: 0–1000. Default: 100.

| Range | Effect |
|-------|--------|
| 0–100 | Photorealistic, literal interpretation |
| 100–300 | Balanced (default zone) |
| 300–600 | Increasingly artistic |
| 600–1000 | Heavily stylized, abstract |

V8 note: Effective range is narrower (100–400 recommended). Extreme values less impactful than V7.

---

## Chaos
`--c VALUE` or `--chaos VALUE`

Range: 0–100. Default: 0.

Controls variety across the 4-image grid. Higher = more diverse results per batch.
- 0–25: Subtle variation
- 25–50: Noticeable diversity
- 50–100: Wildly different outputs

Use for exploration and discovering unexpected compositions.

---

## Weird
`--w VALUE` or `--weird VALUE`

Range: 0–3000. Default: 0.

Pushes results toward unconventional, surreal aesthetics.
- 0–200: Subtle quirks
- 200–800: Tastefully strange
- 800–3000: Full surrealism

Best combined with `--chaos` for maximum experimentation.

---

## Experimental
`--exp VALUE`

Range: 0–100. Available on V7 and V8.

Enhanced detail parameter. Sweet spot is 10–25 for most prompts. Higher values increase fine detail but can over-process.

---

## Quality
`--q VALUE` or `--quality VALUE`

Controls rendering time and detail level (NOT resolution).
- `--q 0.25`: Draft quality, fastest
- `--q 0.5`: Half quality
- `--q 1`: Default
- `--q 4`: Extra coherence (V8 only, 4× cost)

---

## Seed
`--seed VALUE`

Range: 0–4294967295. Default: random.

Same seed + same prompt = similar results. Essential for controlled A/B testing.

**Workflow:**
1. Generate an image you like
2. Note the seed (envelope emoji in Discord, or check job details on web)
3. Modify ONE element of the prompt
4. Regenerate with same seed
5. Compare to isolate the effect of your change

**Caveats:** Avoid Turbo mode with seeds (unreliable). Seeds don't guarantee identical results across model versions.

---

## No (Negative)
`--no ELEMENT1, ELEMENT2`

Excludes elements from the image. Equivalent to a -0.5 weight.

```
forest landscape --no people, buildings, text
```

**Best practices:**
- Start with one term, add more incrementally
- Use catch-all terms ("headgear" vs "hat, cap, beanie, helmet")
- Don't conflict with positive prompt
- In V7+, always use `--no` instead of "without X" in prompt text

---

## Style Raw
`--style raw`

Reduces Midjourney's default aesthetic "polish". Gives more literal, authentic results. Especially useful in V8 Alpha to counter the hyper-polished default. Good for:
- Documentary/photojournalism
- Gritty realism
- Product photography
- When the AI aesthetic is too strong

---

## Stop
`--stop VALUE`

Range: 10–100. Default: 100. Available on V7, V8, and Niji.

Halts generation before completion. Lower values = more abstract, impressionistic results. Useful for creating artistic base images or painterly effects.

---

## Tile
`--tile`

Available on V7 and Niji. Creates seamless repeating tiles. Great for fabrics, wallpapers, patterns. Don't upscale if you need the tile to remain perfectly seamless.

---

## Repeat
`--r VALUE` or `--repeat VALUE`

Available on V7, V8, and Niji. Batch-generates multiple variations of the same prompt. Allowed count depends on plan tier. Fast/Turbo mode only.

---

## Draft Mode
`--draft`

Available on V7. Generates images at ~10× speed and half GPU cost. Results are lower fidelity but ideal for rapid iteration — use draft mode to explore compositions and concepts before committing to full-quality renders.

---

## Personalization
`--p`

Available on V7 (on by default), V8. Adjusts outputs toward your personal aesthetic preferences based on your ranking history on midjourney.com. Toggle off to get the model's default aesthetic. Requires having ranked enough images to build a preference profile.

---

## Moodboards
Moodboards are curated image collections created on midjourney.com. You can reference a moodboard URL alongside `--sref` in a single prompt to blend multiple style influences. Available on V7 and V8.

Use `--sv 7` (V8) for 4× faster style reference/moodboard processing.

---

## Image Weight
`--iw VALUE`

Range: 0–3. Default: 1.

Controls influence of image prompts on the result:
- 0.5: Light influence, mostly follows text
- 1: Balanced (default)
- 2–3: Strong image influence, text is secondary

---

## Version & Model
`--v VALUE` or `--version VALUE`

| Flag | Model |
|------|-------|
| `--v 8` | V8 Alpha (fastest, best text, native 2K) |
| `--v 7` | V7 default (best photorealism, NLU) |
| `--niji 7` | Niji 7 (anime/manga, clean linework) |
| `--niji 6` | Niji 6 legacy (has --style presets) |

Niji 6 style presets: `--style expressive`, `--style cute`, `--style scenic`, `--style original`

---

## V8-Specific Parameters

| Parameter | Purpose | Cost |
|-----------|---------|------|
| `--hd` | Native 2K resolution (2048px) | 4× |
| `--q 4` | Extra coherence mode | 4× |
| `--sv 7` | New SREF/Moodboard version (4× faster) | varies |

V8 supports: `--chaos`, `--weird`, `--exp`, `--style raw`, `--stylize` (up to 1000), `--p`, `--sref`, moodboards.

---

## Reference System

### Omni Reference (V7)
`--oref [image_url]`
Weight: `--ow 0-1000` (default 100)

Put a specific person or object into your images. Higher weight = more literal match. Costs 2× GPU. Not compatible with vary-region/pan/zoom.

### Style Reference
`--sref [image_url]`
Weight: `--sw 0-1000` (default 100)

Match the look, palette, and feel of a reference image. Works on V7, Niji 7, and V8. Can blend with moodboards in one prompt.

### Character Reference (Niji 6 only)
`--cref [image_url]`
Not available on V7 or Niji 7. Niji 7 will get a more powerful replacement.

---

## Video Parameters

V1 Video Model (launched June 2025). Image-to-video animation.

| Parameter | Purpose |
|-----------|---------|
| `--motion low` | Subtle movement (default) |
| `--motion high` | Bigger camera/character motion |
| `--raw` | Reduces creative flair |
| `--bs N` | Batch size (default 4, reduce to 1-2 to save GPU) |

- Standard/Pro/Mega: HD video (Fast Mode only)
- Pro/Mega only: Relax Mode for video (SD only)
- Start with `--motion low`, increase only if needed
- High motion can produce glitchy movements
