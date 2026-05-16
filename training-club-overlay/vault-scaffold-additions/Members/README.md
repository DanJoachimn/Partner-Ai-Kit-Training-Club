---
type: folder-readme
generated_by: claude-code
---

# Members — one file per active member

This folder holds one markdown file per active member of [CLUB_NAME]. Each file is the AI's working memory about that member — their recent context, their state, their goals, their wins.

## File naming

`[First-Last].md` or `[First].md` if no ambiguity. Examples:
- `Anders.md` (if only one Anders)
- `Anders-Madsen.md` (if disambiguation needed)
- `Sarah-K.md` (if two Sarahs at the club)

## File structure

Every member file follows this template (the AI creates the file when a member is first mentioned in a meaningful way):

```markdown
---
type: member
generated_by: claude-code
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: green | amber | red | new | paused
status_since: YYYY-MM-DD
status_reason: "one-line context"
last_seen: YYYY-MM-DD
joined: YYYY-MM-DD
birthday: MM-DD
training_focus: "HYROX Copenhagen Oct 14" | "general fitness" | "first race"
---

# [Name]

## Quick context
[1-3 sentences: who they are, what they're doing here, what matters to them]

## Training focus
[Their current goal — race they're training for, fitness target, post-injury comeback, etc.]

## Recent context
[What was last discussed. Anything they shared — work, family, injuries, life stuff.]

## Personal notes
[Anything worth remembering: kids' names if they mentioned them, partner's name, profession, where they're from. The stuff that makes a check-in feel personal.]

## Interaction log
<!-- Append-only — each entry is one interaction (check-in sent, conversation had, race signed up to) -->

### YYYY-MM-DD — [event/conversation type]
- Context: [what happened]
- Outcome: [what got decided / what's open]
```

## How the AI uses these files

- **Before drafting any check-in:** read the member's file. No file = ask [PARTNER_NAME] before drafting.
- **Weekly retention review:** scans every file's `status` field to classify into traffic-light buckets.
- **Before [PARTNER_NAME] has a real conversation with a member:** your AI reads the file and surfaces context in one paragraph.
- **When something noteworthy happens to a member:** AI appends to the Interaction log (with [PARTNER_NAME]'s confirmation if it's a meaningful change).

## Hard rules

- **Status changes require confirmation.** AI never silently moves a member between green/amber/red. *"Moving Anders to amber — he hasn't been around for 10 days and last we heard work was eating him. Confirm?"*
- **Interaction log is append-only.** History matters. Never delete entries.
- **Member privacy.** This folder is sensitive. Don't surface member-specific info in shared contexts (e.g., when generating a social post — names go in only with explicit approval per post).
- **No member file = no check-in draft.** Don't fabricate context. Ask [PARTNER_NAME] for the details before drafting.

## Starter state

This folder ships empty. Files get created organically as [PARTNER_NAME] mentions members during kick-off + early sessions.

The first time [PARTNER_NAME] says something like *"Anders has been quiet,"* the AI offers: *"Want me to create a Members/Anders.md file so I can track context about him going forward? I'll start with what you just told me + ask 3 quick questions to round it out."*
