# HTC Kick-off Additions

> Layered on top of the Personal kit's kick-off SKILL.md. The HTC-flavored kick-off adds three new section variants and reframes a few existing ones. AI reads this file during HTC install Stage 8.

---

## How to use this file

When invoking the kick-off skill on an HTC install, the AI:

1. Reads the Personal kick-off SKILL.md as baseline
2. Reads this file's overrides
3. Runs the kick-off with these HTC variants applied

The Personal kick-off has sections A (Infrastructure), B (Voice), C (Projects), C+ (People/Companies/Goals/Constraints/Working style), D (What I won't do), E (First task), F (Going forward).

The HTC version replaces or augments these:

| Section | Personal kit version | HTC version |
|---|---|---|
| A | Infrastructure & safety | **A** Infrastructure & safety + **A+** Club basics |
| B | Voice interview (Deluxe 100Q / Express 5Q) | **B (HTC)** Voice interview tuned for operator + member-facing voices |
| C | Active projects | **C (HTC)** Active fronts (programming block, content cadence, member retention focus) |
| C+ | People + Companies + Goals + Constraints + Working style | **C+ (HTC)** Coaches + Members + Race calendar + Goals + Constraints |
| D | What I won't do | (same as Personal) |
| E | First real task | **E (HTC)** First HTC task — usually a draft check-in or content batch |
| F | Going forward | (same as Personal, with HTC framing) |

---

## Section A+ — Club basics (~3 min, after Personal Section A)

After the Personal kit's infrastructure section completes, ask:

> "Couple of quick basics about the club — these help me know what kind of operation you're running:
>
> 1. **Club name** — what should I call it when I'm drafting content or talking about it?
> 2. **City + location** — where's the gym? Helps me anchor race-calendar awareness (Copenhagen + Stockholm if you're in Scandinavia, Berlin if you're in Germany, etc.)
> 3. **Member count, even rough** — am I working with 30 members, 100, 300? Affects how I scale advice.
> 4. **How long have you been running it?** — opening month, year 2, established 5+ years. Affects what you need most."

Save to `vault/_context/club-about.md` once template is filled in.

Confirm with:

> "✅ Got the basics. From here, I know [CLUB_NAME] is a [N-year-old] HYROX Training Club in [city] with roughly [N] members. Moving on."

---

## Section B (HTC) — Voice interview (replaces Personal Section B)

The Personal kit's voice interview has two paths (B-Deluxe 100Q + B-Express 5Q). For HTC, both paths are available, but the EXPRESS questions are HTC-specific. Replace Personal B-Express questions with these 5:

### B1 (HTC) — The club's energy
> "If [CLUB_NAME] walked into a room, what's the energy? Not generic 'welcoming and motivating' — be specific. Are you the gym that runs on irreverent humor? Quiet competence? Loud and proud? Family-feel? Pick the WORDS that distinguish you from any other HTC."

### B2 (HTC) — The ideal member
> "Tell me about your actual member — not your dream member, but the person who's already at your gym and would be devastated if you closed tomorrow. Where do they shop? What do they do for work? What did they do BEFORE they came to you?"

### B3 (HTC) — Brands you'd kill for tonally
> "Three brands — could be fitness, could be anywhere — whose copy you'd genuinely admire. When you read their stuff, you think 'yes — that's the world [CLUB_NAME] should live in.' Examples that work: TYR's race ads, Nike's race-day social, BarBend's coaching tone."

### B4 (HTC) — Other HTCs whose tone is wrong for yours
> "Two HTCs or fitness brands whose tone GRATES on you. Doesn't have to be HYROX-specific. What's specifically wrong about it?"

### B5 (HTC) — Banned words and tropes
> "Words, phrases, or patterns that — if I ever wrote them in a draft for [CLUB_NAME] — would make you reject the whole draft. The fitness-industry banalities you cringe at. List as many as come to mind."

Same as Personal Express: 5 questions, drafts get pasted into `vault/Brand/Voice guide.md`, `Reference brands.md`, `Do-not-use list.md`.

**Note on Deluxe path:** the 100-question interview is mostly the same as the Personal version — the questions about beliefs, taste, voice, writing mechanics all apply to operators just like creators. About 15 of the 100 questions get HTC-specific overrides (the ones about "writing for clients" become "writing for members," etc.). Use judgment.

---

## Section C (HTC) — Active fronts (replaces Personal Section C)

For HTC operators, the analog of "active projects" is **active fronts of the operation**:

Ask:

> "Three fronts your operation is running right now. Not generic 'we're growing' — be specific:
>
> 1. **Programming front** — what block are you in? Race-anchored? Just maintenance? Anything specific about the next 4-8 weeks of training?
> 2. **Content front** — are you posting consistently, sporadically, behind? What's your gut on what's missing in your content?
> 3. **Retention front** — what's your gut on member health right now? Strong, soft, fading? Anyone you're worried about?
>
> Don't give me MBA answers. Tell me what's actually on your mind about each."

Capture verbatim where possible. These three answers seed:
- **Programming front** → `vault/Programming/notes.md` (the AI's reference for what's happening operationally)
- **Content front** → flags whether `weekly-content-batch` is high priority (if they're behind) or low (if they're consistent)
- **Retention front** → flags which members get prioritized in the first `weekly-retention-review`

---

## Section C+ (HTC) — Coaches, Members, Races (replaces Personal Section C+)

After Section C, if [PARTNER_NAME] still has energy:

> "Three more buckets, 8 minutes, that'll make me genuinely sharp:
>
> 1. **Coaches** — name your team. Anyone on staff I should know? 30 seconds each.
> 2. **Members at risk right now** — 2-4 members you're thinking about. The amber/red bucket. No pressure to be precise; just names + 1-line context for each.
> 3. **Races on the calendar** — what races are members signed up to? Within the next 12 weeks especially. Even rough — 'I think Sarah and Tom are doing Copenhagen but I'd have to check' is fine.
>
> Or skip and we'll fill these in over the next few sessions as they come up naturally. Your call."

If they go through:

**Coaches:** create `Coaches/[name].md` per coach with their template, mark `status: active`.

**At-risk members:** create `Members/[name].md` per member with the template, set `status: amber` or `red` based on what [PARTNER_NAME] says, save the 1-line context as `status_reason`.

**Races:** append to `Events/race-calendar.md` under "Upcoming HYROX races," with members signed up where known.

If they skip: mark `.kick-off-deferred-htc-cplus` flag. The wrap-up skill nudges to fill these within the first week.

---

## Section E (HTC) — First HTC task (replaces Personal Section E)

Instead of the generic "what's your most annoying admin task," ask HTC-specific:

> "Last thing before we wrap onboarding — let's actually use this thing together. Pick one:
>
> - **Draft a check-in for an at-risk member** — I'll use what you told me + the Voice guide draft we just wrote
> - **Draft 3 social posts for the upcoming week** — quick batch, see how it lands in your voice
> - **Build a race-anchored block** — give me a race date + how many sessions per week, I'll draft the 4-week block
> - **Triage your inbox right now** — give me access to your email or paste 5-10 recent threads, I'll sort them
>
> Which sounds most useful right now?"

Run whichever they pick. **Real output, not a demo.** This is the moment the partnership feels real.

After it ships:

> "That's the dynamic. You hand me messy or vague, I hand you a draft, you tweak, we ship. Faster every week."

---

## Section F (HTC) — Going forward

Same Personal kit framing PLUS one HTC-specific add:

> "**Three things to take with you, plus one HTC-specific:**
>
> 1. **Talk to me like a colleague, not Google.** Full sentences, full context.
>
> 2. **Tell me when something matters — that's how I remember.** *'Add to notes: Anders mentioned his start-up is eating him.'* I write it down. Survives.
>
> 3. **Tell me when something is recurring.** If you find yourself asking me to do the same thing every week, *'can we make this a skill?'* I'll turn it into a one-button thing.
>
> 4. **The Coaches own their domains.** When you ask about a member, Community Coach handles it; programming, Coaching Coach; content, Marketing Coach; admin, Ops Coach. You always talk to me — they work in the background. Over time you'll notice which one fires for what.
>
> That's it. Welcome to working with the team."

---

## Hard rules for HTC kick-off

- **HTC operators are time-poor.** If they want to skip Section C+, accept immediately. No nudging.
- **Race dates are facts.** Never invent. If they say "I think Copenhagen is in October," verify with WebFetch from `hyrox.com/events` or ask them to confirm before saving the date.
- **Member privacy starts now.** Member files created during kick-off ship with appropriate privacy: status_reasons that they shared are fine; gossip from other coaches is not.
- **Voice guide gets re-read before EVERY future draft.** Drill this hard in Section F so they know the voice file matters.
