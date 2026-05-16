# INSTALL.md — Live install playbook for the Partner AI Kit (Training Clubs)

> **This file is read by an AI agent (Claude Code) at install time.** A Training Club operator has just pasted a prompt asking you to install. They're a Training Club operator, not a developer. They run programming, retention, marketing, ops — alone or with a small team. They want this working, not configured.

---

## Read this carefully before doing anything

All the hard rules from the Personal kit's INSTALL.md apply here (no jargon, confirm before writing, show don't tell, visible progress, no raw errors, pause for physical actions). The **Skill conventions / approval-gate rule** from the Personal INSTALL.md applies with extra emphasis here — any skill that drafts a member-facing message, modifies member records, or touches money MUST gate behind an explicit operator approval. Member trust is the operator's whole business. Never auto-send. On top of that:

**Training Club-specific hard rules:**

1. **Speak operator language, not developer language.** Use "members," "coaches," "programming," "blocks," "race," "scaling" — not "users," "agents," "workflows," "services."
2. **Reference the HYROX context.** They came to this kit because of HYROX. Lean into it. *"Once you've got this set up, I can build you a 4-week block ending at HYROX Copenhagen — just tell me the date."*
3. **Two-phase install.** This kit layers on top of the Personal kit. First run the Personal install (~15 min), then layer the Training Club overlay (~10 min), then the kick-off interview gets Training Club-flavored variants (~25 min). Total: ~50 min for the deluxe path.
4. **Surface the value early.** Within 5 minutes the operator should see a concrete Training Club use case — *"in 20 minutes you'll be able to ask me to draft a member check-in or build a race-anchored block."*

---

## Install runs in two parts (Part 1 + Part 2)

**This is Part 1 (Foundation).** Fits in a single Pro plan session (~50 min, ~30-45 messages). Ends with an automatic voice-note from the user's AI delivered to their phone via Telegram, referencing their club by name. Part 2 (Reach) is a separate later session — deepens voice, adds premium voices and meeting capture, fills in the Training Club-flavored Section C+ (programming defaults, race calendar, member archetypes), wires up optional Training Club skills.

The Part 1 / Part 2 split is **identical in intent** to the Personal kit's split — keeps the magic-prompt install within Pro plan token + message budgets and gives the user a working foundation before deepening.

---

## Stage 0a — Capability check (~1 min, BEFORE the greeting)

**Before anything else**, verify two Claude capabilities are available. These aren't required, but they make the install much smoother for a non-developer Training Club operator. Most operators don't know to turn them on.

### Check 1 — computer use (so you can open System Settings + screenshot for the operator)

Attempt a no-op screenshot via the `computer-use` MCP. If it succeeds → computer use is on. If it returns a "not available" / "permission denied" / "MCP not connected" error → computer use is off.

If off, tell the operator:

> "Quick capability check before we start. I'd like to enable two things so this install is much smoother for you:
>
> **1. Computer use** — lets me open System Settings, take screenshots to verify things are wired up, and click through native apps for you. Without it, I'll have to ask you to do those steps by hand and describe what you see — slower and more error-prone.
>
> To turn it on: in Claude Code Desktop, open **Settings → Capabilities** (or Settings → Features depending on your version) and toggle **Computer use** (sometimes labelled *'Control my computer'*) to ON. You may need to grant Screen Recording + Accessibility permissions when first asked. Let me know when it's on, or say 'skip' if you'd rather not."

If operator enables it → confirm via a fresh screenshot attempt. If operator skips → continue, but warn at every visual-confirmation step.

### Check 2 — Chrome extension (so you can fill web forms for the operator)

Attempt `mcp__claude-in-chrome__list_connected_browsers`. If it returns a connected browser → extension is installed + paired. If it errors → not installed or not paired.

If not connected, tell the operator:

> "**2. Claude Chrome extension** — lets me fill out web forms for you (Telegram bot creation, ElevenLabs signup, your club CRM if we wire it in later, anything browser-based) instead of asking you to navigate and copy-paste yourself. Saves you a LOT of clicking later in this install.
>
> To install: open Chrome → go to the [Chrome Web Store, search 'Claude'](https://chromewebstore.google.com/search/Claude), and add the official Claude extension. After installing, click the extension icon once in Chrome to pair it with this Claude Code session. Tell me when it's done, or say 'skip' if you'd rather not."

If operator installs → verify pairing via another `list_connected_browsers` call. If skipped → continue, manual mode at web-form steps.

### Why ask both upfront, not later

Asking at install time, after the operator has already committed to running the kit, surfaces these capabilities at the moment they're cheapest to enable. Asking mid-install is too late — operator's already in the middle of something and toggling Claude settings derails the flow.

If both are skipped, the install still works — just with more manual operator actions. Don't gate the install behind these. Don't nag.

---

## Stage 0 — Greeting + tone-setting (~1 min)

Open with Training Club context. Set expectations.

Recommended opening:

> "Hi! I'm about to set up your Partner AI Kit (Training Clubs version) — a Claude-based AI partner built specifically for Training Club operators like you.
>
> The install runs in two parts. **Part 1 — today (~50 min):** foundation, four digital employees, your four Training Club skills, scheduled retention review + content batch jobs, and a voice channel to your phone. Ends with an automatic voice-note from your AI on your phone — proof the whole thing works. **Part 2 — separate session, when you're ready (~30 min):** deepens your AI's voice, adds premium TTS, meeting capture, programming defaults + race calendar, member archetypes, and optional skills.
>
> Here's what's going to happen over the next ~50 minutes in Part 1:
>
> 1. **Security check (~3 min)** — I'll audit both repos (Personal foundation + Training Club overlay) for anything sketchy before any file gets written. Open-source code from the internet deserves a careful read-through first.
> 2. **Personal AI foundation Part 1 (~25 min)** — folder, memory layer, four digital employees, scheduled jobs, Telegram bridge, voice channel, recovery files. Ends with a voice-note from your AI on your phone.
> 3. **Training Club overlay (~10 min)** — Training Club-flavored vault folders (Members, Coaches, Programming, Events), 4 Training Club-specific skills (weekly-retention-review, weekly-content-batch, block-builder, member-checkin-draft), HYROX context template stubs. (The 5 standard subagents — Content, Research, Developer, Assistant, Design — come from the Personal foundation in step 2.)
> 4. **Quick Training Club opener (~8 min, 3 questions)** — name your club, name one active block or focus, and pick how you want me to push back. Just enough so the voice note in step 2 lands as personal. The deep Training Club kick-off (programming defaults, race calendar, member archetypes) is in Part 2.
>
> Total: ~50 min. You'll do nothing technical. I'll show you screenshots, open System Settings for you, and confirm everything before I write any file. By the end, you'll be able to ask me things like 'draft a check-in for Anders' or 'build me a 4-week block ending at HYROX Copenhagen' — and the Sunday retention review + content batch jobs will fire automatically every week.
>
> Want me to start with the security check?"

Wait for go-ahead.

---

## Stage 0.5 — Security audit of BOTH repos (~3 min, BEFORE any install steps)

**This is non-negotiable.** Before doing ANY install action, audit BOTH repos. The Training Club kit pulls from two open-source repos, so both need a clean read-through before anything executes.

### Tell the user what's about to happen

> "Quick safety check before I install anything. I'll clone both repos to a sandbox folder, read every file, and look for anything suspicious. Then I'll tell you in plain English whether it's safe. ~3 minutes — and we only proceed if both audits come back clean."

### Clone both repos to a sandbox

```bash
SANDBOX="$HOME/.partner-ai-kit-audit-$$"
mkdir -p "$SANDBOX"
git clone https://github.com/DanJoachimn/Partner-Ai-Kit-Personal.git "$SANDBOX/personal-kit"
git clone https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club.git "$SANDBOX/training-club-overlay"
```

### Run the audit

Read every file in BOTH `$SANDBOX/personal-kit/` and `$SANDBOX/training-club-overlay/`. Apply the full audit protocol from the Personal kit's `INSTALL.md` Stage 0.5 — same nine checklist items, same red flags, same plain-English reporting rules.

For the Training Club overlay specifically, also check that:

- Training Club skill files (in `training-club-overlay/skills/`) only reference paths within the user's vault (`~/Documents/[AI_NAME]/vault/`) and skill folder (`~/.claude/skills/`)
- Plist templates schedule `claude -p` calls with static prompts — never fetch external URLs at runtime
- Vault scaffold additions (`training-club-overlay/vault-scaffold-additions/`) are pure markdown templates — no executable content

### Report the combined verdict

**If both clean:**

> "✅ Security check complete on both repos.
>
> **Personal kit (foundation):**
> [Same 6-7 bullet summary from Personal INSTALL.md Stage 0.5]
>
> **Training Club overlay:**
> - Training Club skills (weekly-retention-review, weekly-content-batch, block-builder, member-checkin-draft) read and write only inside your vault folder
> - The two scheduled jobs (Sunday night retention review + content batch) call the `claude` CLI with static prompts — they don't fetch external code at runtime
> - Vault scaffold additions (Members/, Coaches/, Programming/, Events/) are pure markdown templates — no executable content
>
> **In case you're wondering if it's safe: I read through both repos and can confirm this kit is safe to install. No red flags. Want me to proceed?**"

**If either has concerns:**

> "⚠️ Security check found something worth flagging in [Personal kit / Training Club overlay / both]:
>
> [List specific findings per repo. Quote suspicious code with file:line.]
>
> **Verdict:** Stop and review, or skip the concerning parts, or proceed anyway?"

### Wait for explicit user confirmation

Do not proceed past Stage 0.5 without an explicit *"proceed"* / *"safe"* / *"go ahead"* / *"install it"*.

### Clean up sandbox

```bash
rm -rf "$SANDBOX"
```

The sandbox is for inspection only. Actual install (Stage 1 onward) re-clones fresh to the final locations.

### Hard rules

Same as Personal kit's Stage 0.5 — never skip, never bypass, always be specific in findings, always plain English, never raw stack traces.

---

## Stage 1 — Run Personal kit Part 1 (~25 min)

The Training Club kit DOES NOT duplicate the Personal install. Instead, it triggers Personal **Part 1** (Foundation) first.

```bash
# Clone the Personal kit
mkdir -p "$HOME/Documents/[AI_NAME]"
cd "$HOME/Documents/[AI_NAME]"
git clone https://github.com/DanJoachimn/Partner-Ai-Kit-Personal.git .kit
```

Then read and execute Personal Part 1:

```bash
cat "$HOME/Documents/[AI_NAME]/.kit/INSTALL.md"
```

That's the Personal kit's Part 1 (Foundation) playbook. Run **all** of its stages — but with these two adjustments because we're inside the Training Club install:

- **Skip Personal Stage 0.5** (security audit) — we already ran the combined audit covering both repos in Training Club Stage 0.5 above. Don't repeat it; the user has already confirmed safe-to-install.
- **Personal Stage 5 (the 3-Q lightweight kick-off)** runs as written, EXCEPT pause before the question about "active project" — instead use the Training Club-flavored opener variant in Training Club Stage 7 below. (This swap is intentional: the 3-Q kick-off needs Training Club framing so the Stage 8 aha-moment voice note can reference the user's club + active block.)

When Personal Part 1 Stages 0-9 are done — including the Telegram bridge, voice setup, and the **voice-note aha-moment** in Personal Stage 8 — confirm:

> "✅ Personal AI foundation installed. Folder created, vault scaffolded, four digital employees on standby, Telegram bridge wired, voice channel live, voice-note aha-moment delivered. Now layering on the Training Club stuff."

**Important:** at this point, the Personal kit's Stage 9 has NOT yet set `.part-1-complete`. That gets set at the **end** of the Training Club Part 1 install (Stage 8 below), once the Training Club overlay is fully layered on. This keeps "Part 1 complete" a single, accurate marker.

---

## Stage 2 — Clone the Training Club overlay (~30 sec)

```bash
mkdir -p "$HOME/Documents/[AI_NAME]/.training-club-overlay"
git clone https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club.git "$HOME/Documents/[AI_NAME]/.training-club-overlay"
```

Confirm:

> "✅ Fetched the Training Club overlay — 4 Training Club skills, Training Club-flavored vault additions, HYROX context templates."

(Note: subagents are NOT installed at this stage. The 5 standard subagents — Content, Research, Developer, Assistant, Design — were already installed by the Personal kit foundation in Stage 1. Training Club inherits those; we just add Training Club-specific skills + scaffold on top.)

---

## Stage 3 — Install the Training Club Day-1 skills (~20 sec)

```bash
OVERLAY_SKILLS_SRC="$HOME/Documents/[AI_NAME]/.training-club-overlay/training-club-overlay/skills"
SKILLS_DST="$HOME/.claude/skills"

for skill in weekly-retention-review weekly-content-batch block-builder member-checkin-draft; do
  cp -R "$OVERLAY_SKILLS_SRC/$skill" "$SKILLS_DST/$skill"
  find "$SKILLS_DST/$skill" -type f -name "*.md" -exec \
    perl -i -pe "s/\[AI_NAME\]/[AI_NAME]/g; s/\[PARTNER_NAME\]/[PARTNER_NAME]/g; s/\[CLUB_NAME\]/[CLUB_NAME_PLACEHOLDER]/g;" {} \;
done
```

(Note: `[CLUB_NAME]` placeholder gets filled in during the kick-off interview, so leave as a placeholder for now.)

Confirm:

> "✅ Installed 4 Training Club-specific skills:
> - `weekly-retention-review` — Sunday-night member-risk dashboard
> - `weekly-content-batch` — Sunday-night batch of 7 days of social posts
> - `block-builder` — race-anchored training block generator
> - `member-checkin-draft` — personalized check-in message generator"

---

## Stage 4 — Install scheduled jobs for Training Club skills (~10 sec)

Two Training Club skills run on schedule:

- `weekly-retention-review` — Sunday 19:00
- `weekly-content-batch` — Sunday 20:00

Render and load their plists:

```bash
USER=$(whoami)

for skill_with_schedule in weekly-retention-review weekly-content-batch; do
  PLIST_SRC="$HOME/.claude/skills/$skill_with_schedule/$skill_with_schedule.plist.template"
  PLIST_DST="$HOME/Library/LaunchAgents/com.${USER}.[AI_NAME].$skill_with_schedule.plist"
  sed -e "s/\[USER\]/$USER/g" -e "s/\[AI_NAME\]/[AI_NAME]/g" "$PLIST_SRC" > "$PLIST_DST"
  launchctl load "$PLIST_DST"
done
```

Confirm:

> "✅ Two weekly jobs wired up:
> - Sunday 19:00 → weekly retention review (you'll find it in your inbox / chat history Monday morning)
> - Sunday 20:00 → next week's social posts drafted for review"

---

## Stage 5 — Add Training Club-specific vault folders (~10 sec)

```bash
ADDITIONS_SRC="$HOME/Documents/[AI_NAME]/.training-club-overlay/training-club-overlay/vault-scaffold-additions"
VAULT="$HOME/Documents/[AI_NAME]/vault"

for folder in Members Coaches Programming Events; do
  cp -R "$ADDITIONS_SRC/$folder" "$VAULT/$folder"
done
```

Confirm with diagram:

```mermaid
graph TD
    V[~/Documents/[AI_NAME]/vault/] --> M[Members/<br/>one file per member]
    V --> C[Coaches/<br/>your team]
    V --> P[Programming/<br/>blocks + scaling library]
    V --> E[Events/<br/>races + comps]
    V --> OTHER[(plus Brand, Memory,<br/>Projects, etc. from<br/>the Personal kit)]
```

> "✅ Added Training Club-flavored folders. `Members/` will fill up as we talk about your members; `Programming/` holds your blocks + scaling templates; `Events/` tracks races your members are signed up to."

---

## Stage 6 — Apply Training Club context templates (~5 sec)

The Training Club overlay has Training Club-aware starter templates for the brand voice doc, ICP, and a starter "About this club" file.

```bash
TEMPLATES_SRC="$HOME/Documents/[AI_NAME]/.training-club-overlay/training-club-overlay/context-templates"
CONTEXT_DST="$HOME/Documents/[AI_NAME]/vault/_context"

mkdir -p "$CONTEXT_DST"

for template in club-about brand-voice-training-club ideal-member-profile race-calendar-starter; do
  if [ ! -f "$CONTEXT_DST/$template.md" ]; then
    cp "$TEMPLATES_SRC/$template.md" "$CONTEXT_DST/$template.md"
  fi
done
```

(Only copies if file doesn't already exist — preserves any pre-existing context.)

Confirm:

> "✅ Seeded Training Club context templates. The kick-off interview next will fill them in with your specifics."

---

## Stage 7 — Training Club-flavored 3-Q opener (~8 min, deferred deep kick-off to Part 2)

The deep Training Club kick-off (programming defaults, race calendar, member archetypes, full voice interview) is **deferred to Part 2** to keep Part 1 within a single Pro session. In Part 1 we run just three questions — enough to make the Stage 8 voice-note aha-moment land as personal and to seed the vault with club context.

These three questions REPLACE the equivalent generic 3-Q in Personal Stage 5 (the install playbook deliberately routed there to here).

### Question 1 — Club name + tone

> "**What's your club called, and how should I sound when I talk about it?** Club name first (so I stop saying 'your club' generically). Then three words or one sentence on tone — examples: *'warm-direct, no fluff'* / *'sharp coach, push back on me'* / *'friendly, never corporate.'*"

Save:
- Club name → `~/Documents/[AI_NAME]/vault/_context/club-about.md` (top of file, replaces the placeholder `[CLUB_NAME]`)
- Tone → `~/Documents/[AI_NAME]/vault/Brand/Voice guide.md`

Also: run a placeholder substitution across the 4 Training Club skill files installed in Stage 3 — replace `[CLUB_NAME_PLACEHOLDER]` with the real club name:

```bash
find ~/.claude/skills/{weekly-retention-review,weekly-content-batch,block-builder,member-checkin-draft} \
  -type f -name "*.md" -print0 | \
  xargs -0 perl -i -pe "s/\[CLUB_NAME_PLACEHOLDER\]/$CLUB_NAME/g"
```

### Question 2 — Active block or focus

> "**One active block or training focus right now** — two sentences. Could be a race-anchored block (*'8-week block ending at HYROX Copenhagen Oct 14'*), a general phase (*'strength block, no race target yet'*), or whatever you're running. Just enough that the voice note I send you in a few minutes can mention it."

Save to `~/Documents/[AI_NAME]/vault/Projects/Current block.md` with frontmatter.

### Question 3 — Working style preference

> "**When I'm working with you, do you want me to push back when I disagree, or just deliver what you asked for?** No wrong answer — operators split about 50/50 on this."

Save to `~/Documents/[AI_NAME]/vault/Working style.md` (one-line note).

### Set the deferred-deep-kick-off marker

```bash
# Part 2 will pick up the deeper Training Club kick-off (Section C+ — programming
# defaults, race calendar, member archetypes, full 5-Q voice).
touch "$HOME/Documents/[AI_NAME]/.training-club-kick-off-cplus-pending"
```

---

## Stage 8 — Mark Part 1 complete (~30 sec)

Now wire up the same Part 1 completion flags Personal uses, plus a Training Club-specific marker so Part 2 knows to layer on the Training Club additions:

```bash
# Personal Part 1 completion markers (mirror Personal INSTALL.md Stage 9)
touch ~/Documents/[AI_NAME]/.part-1-complete
date -Iseconds > ~/Documents/[AI_NAME]/.part-1-date
touch ~/Documents/[AI_NAME]/.voice-foundation-3q-complete
touch ~/Documents/[AI_NAME]/.first-run-complete

# Training Club-specific marker — Part 2 reads this to know it should layer on
# Training Club additions (Section C+ deep fill) when the user invokes Part 2.
touch ~/Documents/[AI_NAME]/.training-club-part-1-complete

cat > ~/Documents/[AI_NAME]/.first-run-log.txt <<EOF
First-run completed via Training Club Part 1 install: $(date -Iseconds)
Voice tier: 3-Q foundation (Training Club-flavored)
Training Club skills installed: weekly-retention-review, weekly-content-batch, block-builder, member-checkin-draft
Vault folders added: Members/, Coaches/, Programming/, Events/
Context template stubs seeded: club-about, brand-voice-training-club, ideal-member-profile, race-calendar-starter
Pending: Part 2 (5-Q voice + Training Club Section C+ deep fill + premium voice + meeting capture + optional skills)
User invokes Part 2 when ready: "run Part 2"
EOF

echo "$(date -Iseconds) — TRAINING CLUB PART 1 COMPLETE" >> ~/Documents/[AI_NAME]/logs/install.log
```

Close with:

> "✅ Part 1 done. You've got:
> - A working Partner AI with four digital employees behind it
> - A voice channel from your phone (Telegram, hands-free)
> - Four Training Club-specific skills installed
> - Weekly retention review firing every Sunday 19:00 (your inbox Monday morning)
> - Weekly content batch firing every Sunday 20:00 (next week's posts drafted for review)
> - Voice-note aha-moment delivered — that's the partnership starting
>
> **What's next:** Part 2 deepens everything — a 5-question voice interview, the deep Training Club kick-off (programming defaults, race calendar, member archetypes), premium voices, meeting capture, and optional skills. When you've used Part 1 for a few days and want more, just say **'run Part 2'**.
>
> For now: try asking me to draft a check-in for one of your members, or what's the most useful thing to spend 15 minutes on right now. That's the dynamic."

---

## Variables this playbook expects

| Placeholder | Source |
|---|---|
| `https://github.com/DanJoachimn/Partner-Ai-Kit-Personal.git` | `https://github.com/DanJoachimn/partner-ai-kit-personal.git` |
| `https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club.git` | `https://github.com/DanJoachimn/partner-ai-kit-training-clubs.git` |
| `https://raw.githubusercontent.com/DanJoachimn/Partner-Ai-Kit-Training-Club/main` | `https://raw.githubusercontent.com/DanJoachimn/partner-ai-kit-training-clubs/main` |
| `[AI_NAME]` | Set during Personal install Stage 1 |
| `[PARTNER_NAME]` | Set during Personal install Stage 5 |
| `[CLUB_NAME]` | Set during Training Club kick-off Section A — leave as placeholder until then |

The four `[*_URL]` placeholders need a search-and-replace before the repo is pushed for the first time.

---

## Failure recovery

Same pattern as Personal INSTALL.md — every failure is recoverable from snapshot. The Training Club overlay specifically:

- If `git clone` of the Training Club overlay fails (Personal install succeeded) → user has a working Personal AI; Training Club overlay can be retried later. Tell them: *"The Personal kit installed clean. The Training Club overlay had a hiccup — your AI still works, just without the Training Club-specific stuff. Tell me 'install Training Club overlay' when you want to try again."*
- If any subagent fails to install → install the rest, log the failed one, tell user *"3 of 4 subagents installed. The Content subagent hit an issue — your AI still works, just without that specialized helper. We can retry it later."*

Half-installed is acceptable as long as it's announced and recoverable. Silent failure is not.

---

*This file is the live Training Club install playbook. Update it when the install flow changes; the next operator's install will get the new version automatically.*
