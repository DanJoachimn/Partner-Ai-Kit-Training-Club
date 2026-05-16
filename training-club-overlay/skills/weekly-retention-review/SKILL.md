---
name: weekly-retention-review
description: Sunday-night automated review of every active member's traffic-light state. Surfaces the top 3-5 members at risk this week, suggests coach check-ins, flags milestones coming up. Fires automatically at Sunday 19:00 via launchd; can also be invoked manually with "run the retention review" or "who's at risk this week." Reads vault/Members/ files + attendance data, hands findings to [PARTNER_NAME] via Telegram + chat.
---

# Weekly Retention Review — Sunday-night member-risk dashboard

## Purpose

Most Training Club operators run retention reactively — they notice a member dropped off after they're already gone. By then it's too late.

This skill flips the loop: every Sunday night, [AI_NAME] reviews every active member's state, surfaces the top 3-5 at risk, suggests coach check-ins, and flags milestones for the coming week. [PARTNER_NAME] starts Monday with a clear picture instead of a reactive scramble.

## When this fires

### Auto-trigger
Sunday 19:00 via launchd. See `weekly-retention-review.plist.template` in this skill folder.

### Manual triggers
[PARTNER_NAME] says any of:
- "run the retention review"
- "who's at risk this week"
- "weekly retention review"
- "Sunday review now"

## How it works

### Step 1 — Read every active Member file

```bash
ls "$HOME/Documents/[AI_NAME]/vault/Members/"*.md
```

For each file, parse the frontmatter:
- `status` (green / amber / red / new / paused)
- `status_since` (date the current status was set)
- `last_seen` (date of most recent attendance, if tracked)
- `name` (display name)

Skip paused members. Include green/amber/red/new.

### Step 2 — Classify into action buckets

**Bucket A: Red (urgent intervention this week)**
- Anyone with `status: red`
- Anyone amber for 14+ days
- Anyone last seen 21+ days ago who isn't paused

**Bucket B: Amber-watching (passive observation)**
- Anyone with `status: amber` for <14 days
- Anyone last seen 7-21 days ago

**Bucket C: New (onboarding-touchpoint week)**
- Anyone with `status: new` (still in first 30 days)
- Surface day-by-day: day 7 check-in, day 14 first-month review, day 21 first-fitness-test offer, day 28 conversion-to-membership ask

**Bucket D: Milestones coming up**
- Birthdays in the next 7 days (read from member files' `birthday:` field if set)
- Class milestones (100/500/1000 classes) coming up in next 30 days
- Race dates in next 14 days for members signed up to races

### Step 3 — Draft the brief

Format (delivered via Telegram + saved to vault):

```markdown
# Weekly Retention Review — Sunday YYYY-MM-DD

**This week's focus: [N] members need real attention.**

## 🔴 Red (urgent — coach intervention this week)
- **Anders** — amber → red. Last seen 18 days ago. Status reason: "[from his file]". **Suggested action:** personal call from [PARTNER_NAME] or his primary coach. Draft message? *yes/no*
- **Sarah** — last seen 22 days ago. No status reason logged. **Suggested action:** quick "miss you" message + ask if everything's OK.

## 🟡 Amber (watching)
- Mark, Lisa, Tom — amber for 5-10 days. No action this week unless they no-show again.

## 🟢 New (onboarding touchpoints due)
- **Maria** (joined 7 days ago) — Day-7 check-in due. Want me to draft?
- **Jonas** (joined 28 days ago) — Conversion-to-membership ask due this week. Want me to draft?

## 🎂 Milestones this week
- **Emma's birthday** — Thursday. Want a personalized message draft?
- **Mike hits 500 classes** — Tuesday. Worth a celebration post + personal note.

## 📅 Races coming up (members signed up)
- **HYROX Copenhagen, Oct 14** — 3 members racing (Sarah, Tom, Lisa). Race-week comms fire Oct 7.

---

**One-button actions:**
- "draft red bucket follow-ups" — drafts personalized messages for all 🔴 members
- "draft new-member touchpoints" — drafts Maria + Jonas messages
- "draft milestone messages" — drafts Emma + Mike messages
- "race week comms early" — fires the Oct 14 race nurture sequence now
```

### Step 4 — Deliver

1. Send to Telegram via `send-telegram-text.sh` (if Telegram is wired up)
2. Also save to vault: `~/Documents/[AI_NAME]/vault/Memory/retention-reviews/YYYY-MM-DD.md`
3. Append a 1-line entry to daily-memory: *"Sunday retention review: 2 red, 3 amber, 2 milestones this week."*

### Step 5 — Wait for [PARTNER_NAME]'s response

When [PARTNER_NAME] replies to one of the one-button actions, hand off to the appropriate skill:
- "draft red bucket follow-ups" → invoke `member-checkin-draft` per red member
- "draft milestone messages" → invoke `win-celebration-draft` per milestone
- "race week comms early" → invoke `race-week-comms`

## Hard rules

- **Read the member's file before classifying them.** Don't classify on attendance alone — the status field is authoritative.
- **Never auto-send messages.** Drafts only. [PARTNER_NAME] reviews + sends.
- **Don't pad red bucket.** If no one's actually red, say so: *"🔴 No red-bucket members this week. Strong week."*
- **Member privacy in shared contexts.** This brief goes to [PARTNER_NAME] only. If the Telegram chat is shared with coaches, redact specific status reasons that came from private member conversations.
- **One brief per Sunday.** Don't re-run mid-week unless [PARTNER_NAME] explicitly asks.

## Setup checklist

The kit's Training Club INSTALL.md handles setup. Verifies:
1. Skill installed at `~/.claude/skills/weekly-retention-review/`
2. Launchd plist installed + loaded for Sunday 19:00
3. Telegram bridge present (or graceful fallback to chat if not)
4. `vault/Members/` exists with at least 1 file (otherwise skill is no-op on first run)

## Smoke test

1. Manually create 3 test member files in `vault/Members/` with varied states
2. Run skill manually: *"run the retention review"*
3. Verify the brief includes the 3 members in the right buckets
4. Verify Telegram delivery (if wired)
5. Verify file landed at `vault/Memory/retention-reviews/YYYY-MM-DD.md`
