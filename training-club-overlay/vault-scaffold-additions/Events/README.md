---
type: folder-readme
generated_by: claude-code
---

# Events — races + competitions + community events

Where [CLUB_NAME]'s event calendar lives. Used by AI for race-anchoring training blocks, generating race-week comms, and surfacing what's coming up in retention reviews + content batches.

## Primary file: `race-calendar.md`

A single file with all upcoming events the club's members are racing at, plus internal comps + community events.

Format:

```markdown
# Race Calendar — [CLUB_NAME]

## Upcoming HYROX races

### HYROX Copenhagen — 2026-10-14
- **City:** Copenhagen
- **Category breakdown:** Open, Pro, Doubles, Doubles Pro, Relay
- **Members signed up:** Sarah, Tom, Lisa, Mark (Pro)
- **Notes:** Local race; multiple members racing; race-week comms fire Oct 7

### HYROX Stockholm — 2026-11-22
- **City:** Stockholm
- **Members signed up:** Tom (Pro), Mark (Pro)
- **Notes:** Doubles event possible

### HYROX Worlds — 2027-06-XX
- **City:** TBA
- **Members likely:** Tom, Sarah (if qualifying)

## Internal comps

### Club Open House — 2026-09-15
- Free community taster session
- Race-prep simulation workout

### End-of-block test — every 4 weeks
- Standard benchmark session (see Programming/benchmarks/)
```

## How the AI uses Events files

- **`block-builder`:** anchors training blocks to a specific race in this calendar.
- **`weekly-retention-review`:** surfaces upcoming races + which members are racing (for race-week comms planning).
- **`weekly-content-batch`:** uses upcoming races as primary content tentpoles.
- **`race-week-comms`:** fires automatically 2 weeks before a known race date in this calendar.

## Hard rules

- **Race dates are facts.** Verify from HYROX official sources before adding. Don't propagate rumored dates.
- **Member sign-ups need confirmation.** Don't list a member as racing without [PARTNER_NAME] confirming.
- **Archived races stay in the file.** Add `## Past races` section at the bottom; move events there after they happen. Past races feed `progress-check` (member trajectory analysis).

## Starter state

This folder ships with a stub `race-calendar.md` that [PARTNER_NAME] fills during kick-off Section C+1 ("upcoming races your members are signed up to").
