---
name: weekly-content-batch
description: Sunday-night batch generation of 7 days of social content for [CLUB_NAME]. Drafts one post per day for the upcoming week, anchored to events (races, comps) and recent member wins. Fires automatically at Sunday 20:00 via launchd; can also be invoked manually with "batch next week's content," "draft the content week," "weekly content batch." Reads Brand/, Events/, and recent wins, drafts in club's voice, surfaces for review.
---

# Weekly Content Batch — 7 days of social posts, drafted Sunday night

## Purpose

Training Club operators are content-starved. They know they should post 4-7 times a week. They don't have time to draft 4-7 times a week. So they post 1-2 times, feel guilty, fall behind, post a flurry, fall behind again.

This skill kills the loop. Sunday night, [AI_NAME] drafts the entire upcoming week's content — anchored to events + member wins from this week — in the club's voice. [PARTNER_NAME] reviews on Monday morning, edits the few that need tweaking, schedules the batch. Done in 20 minutes for the whole week.

## When this fires

### Auto-trigger
Sunday 20:00 via launchd (runs after the retention review at 19:00).

### Manual triggers
- "batch next week's content"
- "draft the content week"
- "weekly content batch"
- "draft this week's posts"

## How it works

### Step 1 — Read the context

Pull in:
- `~/Documents/[AI_NAME]/vault/Brand/Voice guide.md` — the club's voice rules
- `~/Documents/[AI_NAME]/vault/Brand/Do-not-use list.md` — banned phrases
- `~/Documents/[AI_NAME]/vault/Events/race-calendar.md` — upcoming races (especially in next 8 weeks)
- `~/Documents/[AI_NAME]/vault/Memory/long-term.md` — recent member wins, club moments
- This week's daily-memory entries — anything content-worthy that happened

### Step 2 — Pick 7 angles for next week

Distribute across these content types (don't do all of one type — variety > monotony):

| Type | Frequency | What it looks like |
|---|---|---|
| **Race anchor** | 1-2 per week if a race is <8 weeks out | Countdown post, training spotlight tied to race, member-signed-up feature |
| **Member win** | 1-2 per week | A specific member's PR, milestone, first race finish — with their permission |
| **Workout spotlight** | 1 per week | A signature session at [CLUB_NAME] — what makes it work, who shows up for it |
| **Behind the scenes** | 1 per week | Coach perspective, programming logic, why a certain block exists |
| **Community moment** | 1 per week | A class story, a coach-member exchange, an after-class beer moment |
| **Educational** | 1 per week | A specific principle (e.g., "why we test 5k pace every 8 weeks") |
| **Race recap** | When a race just happened | Specific members, their times, their stories |

### Step 3 — Draft each post in the club's voice

For each of the 7 angles, draft:
- **Hook** (first line — earns the second line)
- **Body** (3-6 sentences — specific, not generic; named members where appropriate)
- **CTA** (what we want the reader to do — usually: come try a class, sign up to race, share with a friend)
- **Platform notes** (Instagram caption length is fine; if also for X, shorten to ~250 chars)

Apply the Voice guide religiously. Re-read Brand/Voice guide.md after drafting — if any of the 7 break a rule, rewrite that one BEFORE showing to [PARTNER_NAME].

### Step 4 — Output format

```markdown
# Content Batch — Week of YYYY-MM-DD

## Mon — Race anchor (HYROX Copenhagen, 8 weeks out)
**Hook:** [first line]
**Body:** [3-6 sentences]
**CTA:** [the ask]
**Platform:** Instagram, X
**Member tags needed:** [if any]

## Tue — Member win (Sarah's sub-90 Open)
[...]

## Wed — Workout spotlight (Wyrm — our signature interval day)
[...]

## Thu — Behind the scenes (why we're doing aerobic base in October)
[...]

## Fri — Community moment (Jakob and Mike's post-class debate)
[...]

## Sat — Educational (the 5k pace test)
[...]

## Sun — Race anchor (training week recap → Copenhagen)
[...]

---

**One-button actions:**
- "approve all" — saves all 7 to a content calendar file for scheduling
- "approve all but [N]" — saves, but flag post [N] for rewrite
- "rewrite [N]" — try again on a specific post
- "swap [N] for [topic]" — replace post with a different angle
- "save drafts but I'll review later" — saves to `vault/Brand/content-calendar/YYYY-MM-DD.md` for async review
```

### Step 5 — Save approved batch

When [PARTNER_NAME] approves, write to:
`~/Documents/[AI_NAME]/vault/Brand/content-calendar/YYYY-MM-DD.md`

With frontmatter:
```yaml
---
type: weekly-content-batch
generated_by: claude-code
week_starting: YYYY-MM-DD
status: drafted | approved | scheduled | shipped
posts_count: 7
member_tags_needed: [Sarah, Jakob, Mike]
---
```

Append 1-line entry to daily-memory: *"Drafted 7 posts for week of [date]. Sarah-tag pending approval."*

## Hard rules

- **Read the Voice guide BEFORE drafting, not after.** If you draft first then check, you'll find half the posts need rewriting.
- **Specific over generic.** Names, numbers, dates, exact workouts. Not "another great week of training."
- **Member names only with permission flag.** Any post that names a specific member gets a "member tags needed" note — [PARTNER_NAME] checks with the member before publishing.
- **Variety > monotony.** Don't draft 7 race-countdown posts. Variety across the 7 types is the goal.
- **Banned phrases get rejected internally.** Re-read Do-not-use list before delivery. If any draft uses a banned phrase, rewrite that one.
- **Race weeks are different.** If a race is within 7 days of next week, more posts shift to race anchor — that's the natural editorial reality.

## Setup checklist

Handled by Training Club INSTALL.md. Verifies:
1. Skill at `~/.claude/skills/weekly-content-batch/`
2. Launchd plist for Sunday 20:00
3. Brand/Voice guide.md exists (otherwise the skill warns and asks [PARTNER_NAME] to fill it via kick-off first)
4. Events/race-calendar.md exists (otherwise the skill skips race-anchored content)
