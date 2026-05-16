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

## Stage 0 — Greeting + tone-setting (~1 min)

Open with Training Club context. Set expectations.

Recommended opening:

> "Hi! I'm about to set up your Partner AI Kit (Training Clubs version) — a Claude-based AI partner built specifically for Training Club operators like you.
>
> Here's what's going to happen over the next ~53 minutes:
>
> 1. **Security check (~3 min)** — I'll audit both repos (Personal foundation + Training Club overlay) for anything sketchy before any file gets written. Open-source code from the internet deserves a careful read-through first.
> 2. **Personal AI foundation (~15 min)** — folder, memory layer, scheduled jobs, recovery files.
> 3. **Training Club overlay (~10 min)** — Training Club-flavored vault folders (Members, Coaches, Programming, Events), Training Club-specific skills, HYROX context templates. (The 5 standard subagents — Content, Research, Developer, Assistant, Design — come from the Personal foundation in step 2.)
> 4. **Kick-off conversation (~25 min)** — I get to know you, your club, your members, your voice.
>
> Total: ~53 min. You'll do nothing technical. I'll show you screenshots, open System Settings for you, and confirm everything before I write any file. By the end, you'll be able to ask me things like 'draft a check-in for Anders' or 'build me a 4-week block ending at HYROX Copenhagen,' and I'll actually be useful instead of generic.
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

## Stage 1 — Run the Personal kit install (~15 min)

The Training Club kit DOES NOT duplicate the Personal install. Instead, it triggers the Personal install first.

```bash
# Clone the Personal kit
mkdir -p "$HOME/Documents/[AI_NAME]"
cd "$HOME/Documents/[AI_NAME]"
git clone https://github.com/DanJoachimn/Partner-Ai-Kit-Personal.git .kit
```

Then read and execute the Personal `INSTALL.md`:

```bash
cat "$HOME/Documents/[AI_NAME]/.kit/INSTALL.md"
```

Follow Stages 1-9 of the Personal install — using the Personal kit's rules. **Skip two stages:**

- **Skip Personal Stage 0.5** — the security audit. We already ran the combined audit covering both repos in Training Club Stage 0.5 above. Don't repeat it; the user has already confirmed safe-to-install.
- **Skip Personal Stage 10** — the kick-off hand-off. We're going to run the Training Club-flavored kick-off, not the generic one.

When Personal Stages 0-9 are done, confirm:

> "✅ Personal AI foundation installed. Folder created, vault scaffolded, 5 core skills installed, scheduled jobs wired up. Now layering on the Training Club stuff."

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

## Stage 7 — Hand off to the Training Club-flavored kick-off (~25 min)

Now run the kick-off interview, but with Training Club-specific variants for Section A (club context), Section B (voice — operator + member-facing), and Section C (programming defaults + race calendar).

Read the Training Club kick-off additions:

```bash
cat "$HOME/Documents/[AI_NAME]/.training-club-overlay/training-club-overlay/kick-off-training-club-additions.md" 2>/dev/null
```

Then invoke `~/.claude/skills/kick-off/SKILL.md` with the Training Club additions layered in.

> "OK — technical setup is done. From here we have a 25-min conversation. I'll ask you about your club, your members, your voice, your programming style, your race calendar. By the end, I'll know enough about your operation to actually be useful when you ask me for help.
>
> Ready to start, or want to take a break first?"

If start now → invoke kick-off with Training Club additions.

If break → flag pending:

```bash
touch "$HOME/Documents/[AI_NAME]/.kick-off-pending-training-club"
```

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
