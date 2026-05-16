# INSTALL-PART-2.md — Training Club Part 2 (Reach) install playbook

> **This file is read by an AI agent when the user says "run Part 2" or "continue install" after completing Training Club Part 1.** Days, weeks, or months after Part 1 — doesn't matter. The kit's already in place; this playbook deepens it.

---

## When this fires

User says any of:
- "run Part 2"
- "continue install"
- "let's do Part 2"
- "deepen the setup"
- "more setup"
- "expand my partner"
- "finish the Training Club kick-off"

OR: the AI offers it after the user has been using Part 1 for a few days and seems ready for more (proactive opportunity-spotting moment).

---

## Stage 0 — Greeting + check Part 1 is in place (~30 sec)

```bash
test -f ~/Documents/[AI_NAME]/.training-club-part-1-complete \
  || { echo "Training Club Part 1 not complete; redirect to INSTALL.md"; exit 1; }
```

If Part 1 isn't done → tell user, route them to `INSTALL.md` first.

If done → continue:

> "Good to see you back. Part 2 is where I learn your club deeper. Here's what we'll do (~30 min, ~30 messages, fits comfortably in one Pro session):
>
> 1. **5-question voice interview** — sharper voice profile than Part 1's lightweight one (~10 min)
> 2. **Training Club deep kick-off (Section C+)** — programming defaults, race calendar, member archetypes, your scaling philosophy (~10 min)
> 3. **ElevenLabs upgrade** — premium voices if you want them (~5 min, optional)
> 4. **Granola meeting capture** — auto-record + transcribe member calls + coach syncs (~5 min, optional)
> 5. **Optional skills** — content pipeline, document transformations, others (~varies)
> 6. **Siri & Apple Watch** — last because it's least essential (~10 min, optional)
>
> Ready to start with the voice interview, or want to pick a different stage to go to first?"

---

## Stage 1 — 5-question voice interview (~10 min)

Invoke the kick-off skill's **B-Express** path directly. The skill's flag-aware logic detects `.voice-foundation-3q-complete` exists and offers Express (5-Q) as the upgrade.

```bash
# Skill reads .voice-foundation-3q-complete → routes to "upgrade from 3-Q to 5-Q" framing.
# Run the 5 questions from Section B-Express (B1-B5).
```

The questions are the same as Personal Part 2's voice interview, with one Training Club-flavored variant for B4:

- **B1.** One-line principle — *"If [CLUB_NAME] were a person walking into a room, what's the energy? One sentence."*
- **B2.** Target member — *"Tell me about the actual person who walks into [CLUB_NAME] for the first time. Where do they shop? What do they aspire to? What do they fear about a HYROX-style class?"*
- **B3.** Reference brands — *"Three brands — fitness or anywhere — whose copy you'd genuinely admire."*
- **B4.** Other Training Clubs whose tone is wrong for yours — *"Two Training Clubs or fitness brands whose tone GRATES on you. What's specifically wrong?"*
- **B5.** Banned words / tropes — *"Words, phrases, or patterns that — if I ever wrote them in a draft for [CLUB_NAME] — would make you reject the whole draft."*

Capture answers verbatim. Write to:
- `~/Documents/[AI_NAME]/vault/Brand/Voice guide.md` (overwrite Part 1's 3-Q version)
- `~/Documents/[AI_NAME]/vault/Brand/Reference brands.md`
- `~/Documents/[AI_NAME]/vault/Brand/Do-not-use list.md`

Mark complete:

```bash
touch ~/Documents/[AI_NAME]/.voice-express-complete
```

---

## Stage 2 — Training Club deep kick-off (Section C+, ~10 min)

Read the Training Club kick-off additions for the deeper variants:

```bash
cat "$HOME/Documents/[AI_NAME]/.training-club-overlay/training-club-overlay/kick-off-training-club-additions.md"
```

That file contains the Training Club-flavored Section C+ — four buckets, ~2-3 min each:

- **C+1. Coaches + Members** — name your team and the 3-5 members the AI should know about by name + status. Creates files in `Coaches/[name].md` and `Members/[name].md`.
- **C+2. Programming defaults** — your default block length, scaling philosophy, benchmark cadence. Updates `vault/Programming/README.md` + `scaling-library.md` with operator-specific overrides.
- **C+3. Race calendar** — the 1-3 HYROX races per year that are "ours" (local, traveled to, content-anchored). Updates `vault/Events/race-calendar.md`.
- **C+4. Member archetypes** — the 2-3 archetype patterns at the club ("The Returner," "The First-Racer," etc.) so member-checkin-draft pulls archetype-aware tone. Updates `vault/_context/ideal-member-profile.md`.

Each bucket: ask the questions in the kick-off-additions file, capture answers, draft the file content, **show as a code block in chat** and ask *"save it or review and paste?"* (Hybrid Rule — `_context/` writes are user-gated).

Mark complete:

```bash
rm -f ~/Documents/[AI_NAME]/.training-club-kick-off-cplus-pending
touch ~/Documents/[AI_NAME]/.training-club-kick-off-cplus-complete
```

---

## Stage 3 — ElevenLabs upgrade (optional, ~5 min)

> "You've been using Mac's built-in voices since Part 1. ElevenLabs offers premium voices — more natural, more personality. Free tier covers ~10K characters per month at no cost. Want to set it up?
>
> If yes: I'll walk you through making a free account at elevenlabs.io, getting an API key, and pasting it into your config. ~5 min.
>
> If skip: stay on Mac voices. They work fine; this is purely a quality upgrade."

If yes — follow the same flow as Personal `INSTALL-PART-2.md` Stage 2 (open https://elevenlabs.io, walk through signup, clipboard-transfer API key, test).

Mark complete:

```bash
touch ~/Documents/[AI_NAME]/.elevenlabs-configured
```

---

## Stage 4 — Granola meeting capture (optional, ~5 min)

Especially valuable for Training Club operators: coaching calls, member onboarding calls, sales calls, internal coach syncs all auto-captured.

Same flow as Personal `INSTALL-PART-2.md` Stage 3:

1. User downloads Granola from granola.ai (if not already installed)
2. Grant microphone + system audio permissions
3. AI installs the `granola-sync` skill (already in `~/.claude/skills/` from Part 1)
4. Configure `granola-sync/scripts/config.py` with user's vault path + tag rules — recommend tagging by member name + by class type
5. Test sync — manual run produces files in `vault/Meeting Notes/`
6. Schedule via launchd (12:30 + 17:00 daily)

Mark complete:

```bash
touch ~/Documents/[AI_NAME]/.granola-configured
```

---

## Stage 5 — Optional skills menu (varies)

Training Club-relevant optional skills the user can install now or anytime later:

> "These are skills you can install now or anytime later. Each is independent. Tell me which interest you and I'll install just those — or say 'skip' and we move on.
>
> - **Content pipeline** — multi-stage content production (research → draft → quality → distribute). For Training Clubs publishing newsletter / longer-form regularly (~10 min).
> - **Document transformations** — mines meeting transcripts for case-study material — *'mine my coaching calls this month for testimonial-grade member quotes.'* Pairs with Granola (~5 min).
> - **Hyperframes** — animated explainer videos by conversation. Class promos, race recaps, member spotlights (~5 min).
> - **Video Use** — cut filler words + dead air from recordings. For coach-led IG Reels, member testimonials (~5 min).
> - **Book mirror** — turns books you've read (via Readwise highlights) into chapter-by-chapter synthesis docs. Programming, coaching, retention books (~5 min)."

Install only what user picks.

---

## Stage 6 — Siri & Apple Watch (~10 min, LAST — non-essential)

⚠️ **Most fragile stage — save for last.** iOS Shortcuts behavior changes between Apple releases.

> "Last optional step. Want to add Siri voice control + Apple Watch support? Means you can say 'Hey Siri, [AI_NAME], what's on my plate?' from your watch hands-free while you're between classes. Setup is ~10 min. Skip if you'd rather not deal with it — everything else works without this."

If yes: walk through Personal `guides/09-siri-apple-watch-integration.md`.

Mark complete:

```bash
touch ~/Documents/[AI_NAME]/.siri-configured
```

---

## Stage 7 — Part 2 close

```bash
touch ~/Documents/[AI_NAME]/.part-2-complete
touch ~/Documents/[AI_NAME]/.training-club-part-2-complete
date -Iseconds > ~/Documents/[AI_NAME]/.part-2-date
echo "$(date -Iseconds) — TRAINING CLUB PART 2 COMPLETE" >> ~/Documents/[AI_NAME]/logs/install.log
```

Close with:

> "Part 2 done. Now I really know your club.
>
> **What you have now (beyond Part 1):**
> - A 5-question voice profile — drafts land closer to how you'd actually write
> - Deep Training Club context — coaches by name, key members by status, programming defaults, race calendar, member archetypes
> - Premium voice replies (if you upgraded to ElevenLabs)
> - Meeting auto-capture (if you wired Granola) — every coaching call captured within hours
> - The optional skills you added
> - Siri & Apple Watch (if you set them up)
>
> **What this means for you:**
> - `member-checkin-draft` now writes in archetype-aware tone, not generic
> - `block-builder` knows your default block length, scaling philosophy, and race calendar
> - `weekly-retention-review` understands which coaches own which member relationships
> - Drafts compound week over week — the learnings loop is running
>
> **Example use cases now possible:**
> - *'Mine my coaching calls this week for testimonial-grade member moments.'*
> - *'What's the pattern in what my Returner-archetype members keep asking?'*
> - *'Build me an 8-week block ending at HYROX Copenhagen, scaled to my Sunday class average.'*
> - *'Hey Siri, [AI_NAME] — draft a follow-up for the trial members from this week.'*
>
> **What's next:** the kit gets better over time. Run `/update` to pull new skills as they ship. The 100-question deluxe voice interview is still on the table — that's a separate 90-min sitting, best done a few weeks in when you've watched the AI draft enough to know what's still off."

---

## What's still in your back pocket after Training Club Part 2

| Skill / Feature | When to invoke |
|---|---|
| 100-Q deluxe voice interview | When you've used the AI for a few weeks and want maximum voice fidelity. Separate 90-min session. |
| New skills shipping via `/update` | The kit gets new skills over time. `/update` pulls them. |
| LLM Council | *"council this"* / *"pressure-test this"* for any locked decision with real stakes — locking pricing, deciding to expand to a second location, hiring a head coach, etc. |
| Promote member files | As members come and go, add new files in `Members/` and archive the inactive ones to `Archive/`. |

---

*Part 2 of 2 — Reach (Training Clubs). Part 1 (Foundation) is the prerequisite — see INSTALL.md.*
