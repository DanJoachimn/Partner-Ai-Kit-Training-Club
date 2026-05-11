# Partner AI Kit (Training Clubs)

> The HYROX Training Club-flavored version of the Partner AI Kit. An AI partner built for gym operators — knows your members, your programming, your race calendar, your voice. ~30 minutes from install to your first useful conversation.

---

## What this is

The Personal Partner AI Kit + an HTC overlay. You get everything in the [Personal kit](https://github.com/DanJoachimn/Partner-Ai-Kit-Personal) — voice, memory, scheduled jobs, second brain — plus:

- **4 HTC-specific subagents:** Coaching Coach, Community Coach, Marketing Coach, Ops Coach
- **Day-1 skills tuned for gym operators:** weekly retention review, weekly content batch, race-anchored block builder, member check-in drafter
- **Vault scaffold for gym ops:** Members/, Coaches/, Programming/, Events/ folders pre-built with the right starter templates
- **HYROX brand context** baked into the brand voice layer — race calendar awareness, programming vocabulary, member language
- **Integrations roadmap** for Flexybox, Mindbody, Glofox (the booking platforms most HTC operators actually use)

Open-source, free, MIT-licensed. Built by [All Gravy Agency](https://allgravyagency.com). Given away because the world is better when more HTC operators have a real AI partner instead of trying to bolt ChatGPT onto their workflow.

---

## What you walk away with

A typical day inside this AI:

**Monday 06:30:** AI fires your morning brief — today's classes, who's attending, members flagged amber/red, content scheduled, open threads. Telegram delivery, you read it on the way to the gym.

**Wednesday afternoon, 20 min between classes:** *"Draft 3 Instagram posts about the upcoming Copenhagen race."* AI knows your voice, knows the race date, drafts on your phone, you review and approve.

**Friday evening:** Newsletter routine fires. Pulls this week's race results from members signed up to events, member wins, class highlights — drafts the issue in your voice. Ready for review Saturday morning.

**Sunday night 19:00:** Weekly retention review fires. Traffic-light dashboard — who's at risk, who's on a roll, suggested coach check-ins for the week ahead.

**Anytime mid-day:** *"Add Anders to amber for the week — he seemed off after Wyrm today."* AI logs it. Next time you ask about Anders, that context is there.

You never open a terminal. You talk to your AI like you'd talk to a chief of staff.

---

## How to install

**Prerequisites:**

1. **A Mac** running macOS 14 or later
2. **A Claude subscription** (any tier — Pro covers it)
3. **Claude Code Desktop** installed → [download here](https://claude.com/code)

**The install:**

1. Open Claude Code Desktop
2. Paste the prompt below
3. Hit Enter
4. Answer the questions your new AI asks you (~30 min total — a bit longer than the Personal version because of the HTC overlay)

### The install prompt

```
You're about to install the Partner AI Kit (Training Clubs) for me.
I'm not a developer. I run a HYROX Training Club and want an AI partner
built for my operation.

Please:
1. Fetch the live installer from
   https://raw.githubusercontent.com/DanJoachimn/Partner-Ai-Kit-Training-Club/main/INSTALL.md
2. Read it carefully — it has the full install playbook. The HTC version
   layers on top of the Personal kit, so you'll install both.
3. BEFORE installing ANYTHING, do a security audit of BOTH repos (Personal
   foundation + HTC overlay). Clone each to a sandbox folder, read through
   every file, and look for: files touching paths outside the install
   scope, suspicious network calls, hidden or obfuscated code, privilege
   escalation, credential exfiltration patterns, or anything else a
   careful reader would flag for a non-developer downloading from open
   source. Report back in plain English: "safe to install" or "here's
   what's concerning." Wait for me to confirm before any other step.
4. After I confirm the audit's clean, walk me through the install like
   you're talking to a friend who has never used Claude Code. Show
   screenshots, open System Settings when needed, confirm before each
   file write, use checkmarks for progress.
5. When something needs me to do a physical action (download an app,
   click a button), pause and wait for me to say "done."

Start now.
```

---

## The four subagents

Specialized AI workers your orchestrator calls when the task fits their lane:

### Coaching Coach (your programming partner)
Owns workout programming, race-anchored block design, scaling decisions, athlete progressions. Knows the HYROX events (8 stations + runs), can draft week-by-week training blocks anchored to your members' upcoming races. Catches programming mistakes — *"this block has no aerobic base 3 weeks before race day."*

### Community Coach (your retention partner)
Owns member retention, traffic-light analysis (green/amber/red), birthday/milestone tracking, win-celebration drafting, lapsed-member follow-up. The subagent that knows every member's recent context — so when you ask *"how's Anders been doing?"* you get a real answer.

### Marketing Coach (your content + sales partner)
Owns content calendar, social posts, newsletter drafts, race promo, inquiry responses, trial-conversion follow-ups. Knows your club's voice + the HYROX brand layer. Drafts in your tone, not generic gym-marketing slop.

### Ops Coach (your admin partner)
Owns email triage, calendar management, booking platform integration (Flexybox/Mindbody/Glofox), invoicing follow-ups, supplier management. The "behind the scenes" subagent that keeps your business running while you coach.

---

## The Day-1 skills (more grow over time)

Four skills come pre-installed. Each one is built specifically for HTC operators:

| Skill | Trigger | What it does |
|---|---|---|
| `morning-brief` | Auto 06:30 daily | Today's classes + attendees + members flagged + content scheduled + open threads |
| `weekly-retention-review` | Auto Sunday 19:00 | Traffic-light dashboard, top members at risk, coach check-in suggestions |
| `weekly-content-batch` | Auto Sunday 20:00 OR manual | Drafts 7 days of social posts for review |
| `block-builder` | Manual: *"build me a 4-week block ending at HYROX Copenhagen"* | Race-anchored training block with scaling options |
| `member-checkin-draft` | Auto when member hits amber, or manual: *"draft a check-in for Anders"* | Personalized message in your club's voice, ready to send |

More skills get built **as you notice patterns in your work** — the kit's proactive opportunity-spotting (built into the kick-off and wrap-up flows) surfaces *"hey, you've done this manually 3 weeks running, want me to turn it into a skill?"*

---

## The vault scaffold (gym-flavored)

On install, your vault gets these HTC-specific folders:

```
~/Documents/[your-ai-name]/vault/
├── Members/         ← one file per member, with traffic-light state + recent context
├── Coaches/         ← your team
├── Programming/     ← workout blocks, scaling library, benchmark sessions
├── Events/          ← race calendar, internal comps, community events
└── (plus the Personal kit defaults: Brand/, Projects/, Notes/, Memory/, etc.)
```

The `_context/` layer gets HTC-aware starter templates — your brand voice doc has prompts like *"how do you talk about HYROX races vs general fitness?"* baked in.

---

## Updates

Same `/update` pattern as the Personal kit. Anytime new skills or bug fixes ship to this repo, run:

```
/update
```

Your AI fetches the latest, shows you what's new, asks before changing anything you've tuned.

---

## What's NOT in this kit (yet)

Real talk about the roadmap. These are on the list but not in V1:

- **Flexybox / Mindbody / Glofox MCP integrations** — Coming Q3 2026. Currently the Ops Coach can read your data if you paste/export it; direct API hookup is the next big unlock.
- **HYROX race calendar feed** — Manual entry for now. Live feed planned once HYROX exposes one.
- **Native dashboard UI** — The kit lives entirely inside Claude Code Desktop. A custom dashboard ("Pacer cockpit") is on the roadmap but not blocking — the chat interface is already the primary way operators use it.

---

## License

MIT — fork it, modify it, sell something built on top of it. If you publish something that builds on this, link back so people can find the source.

---

## Help, feedback, bug reports

Open a [GitHub issue](https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club/issues).

Or tell your AI about a bug — it can often diagnose and propose a fix. If the fix is useful for everyone, it can open a PR back to this repo.

---

## Who built this

[All Gravy Agency](https://allgravyagency.com). We work with HYROX Training Clubs on retention, content, and AI-augmented operations. This kit is the install foundation we use for every client engagement — given away free because the HTC space is too small for paywalled tooling and too big for everyone to reinvent the same wheels.

If you want help setting yours up beyond what your AI can do, or you want a custom-built version with your specific integrations + content workflows, [get in touch](https://allgravyagency.com/contact).

---

*Built with [Claude Code](https://claude.com/code). The whole kit was designed in conversation with an AI partner. Recursion is the point.*
