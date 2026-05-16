---
name: member-checkin-draft
description: Generate a personalized check-in message for a specific member in [CLUB_NAME]'s voice. Reads the member's file (recent context, status, last interaction) and the club's brand voice guide, drafts a message that feels human and specific — not templated. Invoked when [PARTNER_NAME] says "draft a check-in for [member]," "follow up with [member]," or auto-invoked by weekly-retention-review for amber/red members.
---

# Member Check-in Draft — personalized, in-voice, ready-to-send

## Purpose

Generic "we miss you!" messages don't work. Members can smell a template. What works: a check-in that references their actual context — what they last said, what they last did, what's going on in their life if they shared it.

This skill closes the gap. [AI_NAME] reads the member's file, the club's voice guide, and any recent shared context. Drafts a message that sounds like [PARTNER_NAME] wrote it after thinking about that member specifically. [PARTNER_NAME] reviews, tweaks if needed, sends.

## When this fires

### Manual triggers
[PARTNER_NAME] says any of:
- "draft a check-in for [member name]"
- "follow up with [member]"
- "message [member] — they've been quiet"
- "I need to reach out to [member]"

### Auto-invocation
`weekly-retention-review` invokes this skill once per amber/red member when [PARTNER_NAME] approves the "draft red bucket follow-ups" action.

## How it works

### Step 1 — Read the member's file

```bash
MEMBER_FILE="$HOME/Documents/[AI_NAME]/vault/Members/[member-name].md"
```

If file doesn't exist:
> "I don't have a file for [member name] yet. Want me to create one? It'd help me draft better check-ins. For now, what do you remember about them — last conversation, what they're training for, anything stressful in their life?"

If file exists, parse:
- `status` (green/amber/red/new/paused)
- `status_since` (when current state was set)
- `status_reason` (one-line context for why)
- `last_seen` (most recent attendance, if tracked)
- `recent_context` (free-form notes from prior conversations)
- `training_focus` (current goals if logged — e.g., "HYROX Copenhagen Oct 14")
- `personal_notes` (anything they shared — health, family, work, etc.)

### Step 2 — Read the brand voice context

- `~/Documents/[AI_NAME]/vault/Brand/Voice guide.md` — how [CLUB_NAME] sounds
- `~/Documents/[AI_NAME]/vault/Brand/Do-not-use list.md` — banned phrases

### Step 3 — Draft the message

Structure:
1. **Open with their name and a real callback** — not "hey member." Reference their last real moment: race they ran, conversation you had, milestone they hit, thing they're training for.
2. **Acknowledge the absence/situation without dramatizing** — if they're amber, the message acknowledges the gap without making it heavy. "Missed you this week" not "we're SO worried about you."
3. **Make it easy to respond OR easy to come back** — give one clear path forward. Either an invitation ("class Thursday — Sled Volume Day, your kind of mess") or an open door ("no pressure to reply, just wanted you to know I noticed").
4. **Sign off in [PARTNER_NAME]'s name, not the club's.** Personal feels personal.

### Step 4 — Apply the Voice guide

Before showing the draft to [PARTNER_NAME], re-read Brand/Voice guide.md and verify:
- No banned phrases from `Do-not-use list.md`
- Tone matches what's documented in `Voice guide.md`
- Length feels right for the medium (shorter for Telegram/SMS, can be longer for email)

If anything's off, rewrite BEFORE showing.

### Step 5 — Show the draft + delivery options

```markdown
**Draft check-in for [member name]:**

> Hey [name] —
>
> [The drafted message — typically 3-6 sentences]
>
> — [PARTNER_NAME]

**Delivery options:**
- Channel: SMS / WhatsApp / Email / In-person next class
- Length: looks good / make it shorter / make it longer
- Tone: looks good / warmer / more direct
- Specific edit: "change [X] to [Y]"
- "send it" — copies to clipboard, you paste into your messaging app
```

### Step 6 — Log the interaction

Once [PARTNER_NAME] confirms sent (or chooses "send it"), log to the member's file:

```bash
# Append to Members/[member-name].md under "## Interaction log"
echo "
### YYYY-MM-DD — Check-in sent by [PARTNER_NAME]
- Trigger: [amber/red bucket | one-off ask]
- Sent via: [SMS/WhatsApp/Email/In-person]
- Message summary: [first 2 sentences]
- Awaiting response: yes
" >> "$MEMBER_FILE"
```

Bump `updated:` in member file's frontmatter.

Also append to daily-memory: *"Drafted + sent check-in to [name] (amber bucket)."*

### Step 7 — Suggest follow-up timing

If member is amber/red, propose:

> "If [name] doesn't respond within 5 days, I'll surface this in next Sunday's retention review for a second touchpoint. If they respond, tell me how it went and I'll update their status."

## Examples (good vs bad)

**❌ Generic (rejected by this skill before showing to [PARTNER_NAME]):**
> "Hey [name], we miss you at the gym! Hope you're doing well. Come back soon — we have lots of great classes for you."

**✅ Specific (passes voice check):**
> "Hey Anders —
>
> Noticed you haven't been around since the work-stress thing you mentioned a couple weeks back. No pressure, just thinking of you. The Wyrm session lands Thursday if you want a real reset — that's your favorite. Or beer after if you'd rather skip the gym and just catch up.
>
> — [PARTNER_NAME]"

The second version reads as: actual person → who knows Anders → wrote this in 30 seconds → because Anders matters.

## Hard rules

- **Read the member file first. Always.** No file = ask before drafting.
- **Read the Voice guide BEFORE drafting.** Templates don't work; voice does.
- **Never reveal you know data the member didn't share.** "I see you've been amber for 14 days" is wrong. "Noticed you've been quiet" is right.
- **Personal sign-off, not corporate.** [PARTNER_NAME] signs, not "[CLUB_NAME] Team."
- **No emotional manipulation.** "We're worried about you" is heavy and presumptuous. "Just thinking of you" lands lighter.
- **One ask per message, max.** Either invite to a specific class OR open door — not both. Choice overload = no response.
- **Never auto-send.** Drafts only. Always.

## Smoke test

1. Create a test member file `vault/Members/test-anders.md` with `status: amber, status_reason: "work stress, mentioned 2 weeks ago"`
2. Run: *"draft a check-in for Anders"*
3. Verify the draft references "work stress" callback
4. Verify it follows the club's voice (or warns if Voice guide.md is empty)
5. Verify the interaction logs to the member file after "send it"
