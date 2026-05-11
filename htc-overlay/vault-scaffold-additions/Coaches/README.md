---
type: folder-readme
generated_by: claude-code
---

# Coaches — your team

One file per coach at [CLUB_NAME]. Used by the AI to understand which coach handles which members, which classes, which programming styles.

## File structure

```markdown
---
type: coach
generated_by: claude-code
created: YYYY-MM-DD
updated: YYYY-MM-DD
role: head-coach | coach | assistant-coach | guest
status: active | inactive
joined: YYYY-MM-DD
---

# [Coach Name]

## Specialties
[What they're known for at the club — programming style, HYROX expertise, strength focus, mobility, etc.]

## Classes they lead
[Days/times if relevant, or "all classes" or "weekend specialist"]

## Members they have a primary relationship with
<!-- The members they're the go-to coach for — useful for routing check-ins -->

## Communication preferences
[How they want to be reached. Voice/text/email. When they're off-duty.]

## Notes
[Anything else worth remembering — coaching philosophy, certifications, race history]
```

## How the AI uses these files

- **Routing check-ins:** when Community Coach drafts a member check-in, it considers which coach has the primary relationship.
- **Class brief generation:** Coaching Coach checks who's leading the class today.
- **Schedule conflicts:** Ops Coach uses coach availability when proposing class schedule changes.

## Hard rules

- **Coaches are people, not labels.** Their files get the same care as member files.
- **Communication preferences are respected.** If a coach says "only reach me Mon-Fri 9-5," the AI doesn't surface non-urgent things outside that window.

## Starter state

Empty. [PARTNER_NAME] populates during kick-off (Section A or C+1 — "name 3-5 people I should know about").
