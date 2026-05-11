# UPDATE.md — Live update playbook for the Partner AI Kit (Training Clubs)

> Same shape as the Personal kit's UPDATE.md, but updates BOTH the Personal foundation AND the HTC overlay. Read by the `/update` skill when an HTC user runs `/update`.

---

## When this fires

User says any of:
- `/update`
- "update my AI"
- "update my kit"
- "check for kit updates"

(All these triggers route through the existing `/update` skill — which detects whether the install is Personal-only or HTC-flavored by checking for `~/Documents/[ai-name]/.htc-overlay/` and switches playbooks accordingly.)

---

## The HTC update flow

### Step 1 — Announce + check both repos

```
Checking both repos:
- Personal kit (foundation) — fetching from https://raw.githubusercontent.com/DanJoachimn/Partner-Ai-Kit-Personal/main
- HTC overlay — fetching from https://raw.githubusercontent.com/DanJoachimn/Partner-Ai-Kit-Training-Club/main

Comparing to what's installed...
```

### Step 2 — Snapshot both checkouts

```bash
cd "$HOME/Documents/[AI_NAME]/.kit"
PERSONAL_COMMIT=$(git rev-parse HEAD)

cd "$HOME/Documents/[AI_NAME]/.htc-overlay"
HTC_COMMIT=$(git rev-parse HEAD)

echo "Personal kit commit: $PERSONAL_COMMIT" > "$HOME/Documents/[AI_NAME]/_recovery/pre-update-snapshot.txt"
echo "HTC overlay commit: $HTC_COMMIT" >> "$HOME/Documents/[AI_NAME]/_recovery/pre-update-snapshot.txt"
echo "Timestamp: $(date -Iseconds)" >> "$HOME/Documents/[AI_NAME]/_recovery/pre-update-snapshot.txt"
```

### Step 3 — Run Personal kit update first

Read the Personal kit's `UPDATE.md`:

```bash
cat "$HOME/Documents/[AI_NAME]/.kit/UPDATE.md"
```

Run that playbook. If it fails, abort — don't proceed to HTC overlay until Personal is on solid ground.

### Step 4 — Categorize HTC overlay changes

After Personal kit update completes, fetch HTC overlay diff:

```bash
cd "$HOME/Documents/[AI_NAME]/.htc-overlay"
git fetch origin main
NEW_HTC_COMMIT=$(git rev-parse origin/main)

if [ "$HTC_COMMIT" = "$NEW_HTC_COMMIT" ]; then
  echo "HTC overlay already on latest. Nothing to update."
fi

git log --oneline "$HTC_COMMIT..$NEW_HTC_COMMIT"
git diff --name-status "$HTC_COMMIT..$NEW_HTC_COMMIT"
```

### Step 5 — Apply HTC overlay changes

Same categorization rules as Personal UPDATE.md, applied to HTC-overlay file paths:

| Change type | Action |
|---|---|
| `htc-overlay/subagents/[coach].md` modified | Update the coach's file in `~/Documents/[AI_NAME]/.claude/agents/` (with consent if tuned via learnings) |
| `htc-overlay/subagents/[new-coach].md` added | Offer the new coach. Rare — the 4 coaches are stable; new ones are major events |
| `htc-overlay/skills/[skill]/SKILL.md` modified | Update the user-level skill in `~/.claude/skills/` (with consent if tuned) |
| `htc-overlay/skills/[new-skill]/` added | Offer the new skill. This is the most common HTC update — new operational skills shipping |
| `htc-overlay/skills/[skill]/[skill].plist.template` modified | Re-render the plist, reload the launchd job |
| `htc-overlay/vault-scaffold-additions/[folder]/` modified | Skip — these only matter for new installs. Mention in summary. |
| `htc-overlay/vault-scaffold-additions/[new-folder]/` added | Offer to add the new folder to user's vault |
| `htc-overlay/context-templates/[file]` modified | Skip — only seeded once at install time. Mention in summary. |

### Step 6 — Apply approved updates

Same as Personal UPDATE.md — apply changes, preserve tunings, re-render plists where needed.

### Step 7 — Fast-forward both checkouts

```bash
cd "$HOME/Documents/[AI_NAME]/.kit" && git pull origin main
cd "$HOME/Documents/[AI_NAME]/.htc-overlay" && git pull origin main
```

### Step 8 — Combined summary

Tell the user in plain English what changed across both repos:

```markdown
✅ Update complete (Personal + HTC).

**Personal kit:**
- [N] skill updates: [list]
- [N] new skills offered: [list]

**HTC overlay:**
- [N] coach updates: [list]
- [N] HTC skill updates: [list]
- [N] new HTC skills: [list]

**Now running:**
- Personal kit: [PERSONAL_SHORT_HASH] (was [OLD_PERSONAL_SHORT_HASH])
- HTC overlay: [HTC_SHORT_HASH] (was [OLD_HTC_SHORT_HASH])
```

---

## Failure recovery

Same as Personal UPDATE.md — every failure path is recoverable from `pre-update-snapshot.txt`. Both commits get rolled back together if anything goes sideways during reconciliation.

If Personal update succeeds but HTC update fails:
- Personal kit is on the new commit
- HTC overlay rolls back to its pre-update commit
- User has a working install with mismatched versions; they can retry HTC update later

Tell user explicitly:
> "Personal kit updated cleanly. HTC overlay hit a snag — rolled it back so it's at the previous version. Your AI still works; the HTC-specific stuff just isn't on the latest version. Run `/update` again to retry the HTC piece."

---

## Hard rules (same as Personal UPDATE.md)

- **Never silently overwrite tuned skills/subagents.**
- **Never modify user vault content.** Only add new scaffold folders with consent.
- **Always snapshot before pulling.** Both commits.
- **Plain English summaries.** No raw git output unless user asks.
- **Updates are opt-in for additions, opt-out for fixes.**

---

## Variables this playbook expects

| Placeholder | Source |
|---|---|
| `[AI_NAME]` | Read from `~/Documents/*/CLAUDE.md` frontmatter |
| Personal repo URL | Already baked into `~/Documents/[ai-name]/.kit/.git/config` (`https://github.com/DanJoachimn/Partner-Ai-Kit-Personal.git`) |
| HTC repo URL | Already baked into `~/Documents/[ai-name]/.htc-overlay/.git/config` (`https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club.git`) |
