---
name: block-builder
description: Generate a race-anchored training block (4 / 8 / 12 weeks) ending at a specific HYROX race date. Includes weekly periodization (base → build → peak → taper), session-by-session work, scaling options (Pro / RX / Scaled), and benchmark sessions every 3 weeks. Invoked when [PARTNER_NAME] says "build me a [N]-week block ending at HYROX Copenhagen," "draft a race block for [member]," "what should our programming look like for the next 8 weeks." Coaching Coach owns this skill.
---

# Block Builder — race-anchored training blocks

## Purpose

Generic gym programming doesn't anchor to anything. HYROX programming should — every session is a step toward a specific race date. Without a tool, [PARTNER_NAME] either programs week-by-week reactively or copies someone else's block that doesn't fit their members.

This skill generates a full block (4/8/12 weeks) anchored to a known race date, with the right periodization shape, weekly work distribution, and scaling tiers built in. [PARTNER_NAME] reviews + tweaks, and they've got a coaching plan instead of a guess.

## When this fires

[PARTNER_NAME] says any of:
- "build me a [N]-week block ending at HYROX Copenhagen"
- "draft a race block for [member name]"
- "what should our programming look like for the next [N] weeks"
- "block builder for [date]"
- "race anchor a block to [date]"

## How it works

### Step 1 — Confirm inputs

If any of these are missing, ask:

1. **Block length** — 4, 8, or 12 weeks? (Default: 8 if not specified.)
2. **End date** — the race or target date? Read from `Events/race-calendar.md` if mentioned by name (e.g., "Copenhagen") or ask explicitly if not findable.
3. **Sessions per week** — default 4 if not specified. Ask only if ambiguous.
4. **Target population** — class-wide program (default), specific member, or specific group (Open Pro, Doubles team, etc.)?
5. **Starting fitness baseline** — if specific member or group, do their benchmark numbers exist in `vault/Members/[name].md` or `vault/Programming/benchmarks/`? If yes, anchor to their numbers; if no, work from generic "intermediate HYROX athlete" assumptions and flag the assumption.

### Step 2 — Determine periodization phase distribution

Standard HYROX block shape (adapt per length):

| Block length | Base | Build | Peak | Taper |
|---|---|---|---|---|
| 4 weeks | — | 2 weeks | 1 week | 1 week (5-7 days) |
| 8 weeks | 2 weeks | 4 weeks | 1 week | 1 week (5-7 days) |
| 12 weeks | 4 weeks | 5 weeks | 2 weeks | 1 week (5-7 days) |

**Phase definitions:**
- **Base:** aerobic work, station strength, work capacity. Volume up, intensity moderate. Less race-specific, more general fitness.
- **Build:** race-specific intensity, station-specific strength, mixed-modal sessions. Volume sustained, intensity climbs.
- **Peak:** race simulations, sharpening sessions, race-pace work. Volume drops slightly, intensity high.
- **Taper:** deload. Volume drops 40-50%, intensity stays sharp, recovery prioritized. Race-week is touch-and-go: feel-good sessions, no new stimulus.

### Step 3 — Generate the weekly framework

For each week, output:
- **Phase** (base/build/peak/taper)
- **Theme** for the week (e.g., Week 3 = "Capacity Week — long aerobic work + sled-pull volume")
- **Session-by-session work** (one block per training day; if 4 sessions/week → 4 days of work)
- **Volume target** for the week (in time-under-tension or session count)
- **Key benchmark to test** (every 3 weeks: 5k row, 1k erg, max wall ball set, etc.)

### Step 4 — Generate the sessions

For each session in each week:

```markdown
## Week 3, Session 2 — Build Phase — Sled Volume Day

**Warm-up (10 min):**
- 500m row easy
- 2 rounds: 10 air squats, 10 jumping lunges, 5 burpees

**Main (40 min):**
- 4 rounds for time:
  - 100m sled push (heavy — 1.5x bodyweight)
  - 200m run
  - 100m sled pull
  - 200m run
- Target: 18-22 min total
- Rest 4 min between rounds if athletes need it

**Accessory (10 min):**
- 3x10 KB swings (24/16 kg)
- 3x10 single-arm farmer carry per side (16-24 kg)

**Scaling — Scaled tier:**
- Sled push: bodyweight load instead of 1.5x
- 100m run instead of 200m

**Scaling — Pro tier:**
- 150m sled segments
- Unbroken pace target
```

### Step 5 — Output the full block

```markdown
# 8-Week Block — HYROX Copenhagen — Oct 14

**Generated:** YYYY-MM-DD
**Athletes:** Class-wide / [member name]
**Sessions/week:** 4
**Phase distribution:** 2 base / 4 build / 1 peak / 1 taper

---

## Week 1 (Aug 19-25) — Base Phase — Aerobic Foundation
[full week of sessions]

## Week 2 (Aug 26 - Sep 1) — Base Phase — Station Strength
[full week]

## Week 3 (Sep 2-8) — Build Phase — Sled Capacity
[full week]

[... etc ...]

## Week 8 (Oct 7-13) — Taper Week
[full week — light, sharp, no new stimulus]

**Race day: Oct 14**

---

## Benchmarks to test
- Week 1: 5k row baseline
- Week 4: 1k erg + max wall ball set
- Week 7 (taper): light race simulation (50% volume)

## Scaling tiers documented in
- `vault/Programming/scaling-library.md` (or proposed for creation if missing)
```

### Step 6 — Save + confirm

Save the full block to:
`~/Documents/[AI_NAME]/vault/Programming/blocks/YYYY-MM-DD-to-[race-date].md`

Tell [PARTNER_NAME]:

> "✅ 8-week block drafted, ending at HYROX Copenhagen (Oct 14). Saved to `Programming/blocks/2026-08-19-to-2026-10-14.md`.
>
> **Review priorities:**
> - Week 3-4 sled volume — feels high; want to soften?
> - Benchmarks at Week 1, 4, 7 — does that cadence work for your members?
> - Taper week — I went conservative (40% volume drop). Want sharper?
>
> Tell me what to adjust, or 'approve' to lock it in."

## Hard rules

- **Always anchor to a real race date.** Never invent one. If date isn't found in `race-calendar.md`, ask.
- **Always offer 3 scaling tiers per session.** Pro / RX / Scaled. Not optional.
- **Specific over generic.** Times, distances, loads, reps. "4 rounds: 100m sled push, 200m run, 100m sled pull" — never "do some intervals."
- **Member-anchored blocks read the member file.** If `Members/[name].md` has benchmark data, anchor to their numbers. If not, work from intermediate-athlete assumptions and FLAG that.
- **Taper is non-negotiable.** Even on 4-week blocks. Members racing without a taper risk underperformance + injury. If [PARTNER_NAME] tries to remove taper, push back.
- **Never auto-publish to a programming app.** Save the markdown file; [PARTNER_NAME] copies to TrainingPeaks / WodUp / wherever themselves.

## Smoke test

1. Test with manual invocation: *"build me a 4-week block ending Sept 15 for our class — 3 sessions per week."*
2. Verify the block has correct periodization (no base phase on 4-week → straight into build)
3. Verify each session has warm-up + main + accessory + 3 scaling tiers
4. Verify the file lands at `vault/Programming/blocks/...`
5. Verify [PARTNER_NAME] can ask for tweaks and the block updates in place

## What this skill DOES NOT do

- Doesn't generate one-off workouts (use `class-brief` skill — to be built)
- Doesn't simulate race performance (different skill — race-pace-predictor — roadmap)
- Doesn't auto-publish to programming apps (manual copy to TrainingPeaks / WodUp / etc.)
- Doesn't replace coaching judgment — it's a starting draft, not a final plan
