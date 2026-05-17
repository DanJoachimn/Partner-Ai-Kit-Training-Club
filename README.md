# Partner AI Kit (Training Clubs)

> The Training Club-flavored version of the Partner AI Kit. An AI partner built for Training Club operators — knows your members, your programming, your race calendar, your voice. ~30 minutes from install to your first useful conversation.

---

## Why this exists

Staying current on AI is a full-time job. New models, new tools, new patterns every week. You're running a Training Club — programming, retention, content, ops. You don't have spare hours to chase the AI firehose.

This kit does that job, so you can keep running your club. Claude Code-native, lives on your Mac, and **you own it forever.** No SaaS, no monthly seat, no vendor that disappears with your member data. Open-source. Yours.

The compounding part comes in two layers.

**First — it learns YOUR Training Club.** Out of the box: HYROX programming, race calendar, retention vocabulary. As you go: your members, your voice, your way of running the floor. After a few weeks it stops feeling like a tool and starts feeling like the chief of staff you've been meaning to hire. One who's on duty 24/7 and wears the exec assistant, content manager, ops coordinator, and research lead hats too.

**Second — the kit moves with the AI landscape.** New skills land in this repo. You pull updates with one command. Stay current without becoming an AI hobbyist.

---

## Is this safe to install?

Fair question. The kit is an "outfit" your main AI puts on to work inside your Training Club world — your members, your programming, your voice, your scheduled tasks. Without it, the AI is generic. With it, it's yours.

Three things you should know about safety:

**The kit checks itself before doing anything.** When you paste the install prompt, your AI first reads every file and tells you in plain English whether it's safe. If anything looks off, it stops. You don't have to know what to look for. Your AI does.

**Your passwords stay on your Mac.** They live in a file on your computer, not on someone else's server. Want to remove access? Delete the file.

**You can stop it any time.** It's just files on your Mac. No subscription to cancel. Uninstall is *drag the folder to the trash*.

---

## What this is

The Personal Partner AI Kit + an Training Club overlay. You get everything in the [Personal kit](https://github.com/DanJoachimn/Partner-Ai-Kit-Personal) — voice, memory, scheduled jobs, second brain — plus:

- **The 4 standard subagents** (same as the Personal kit): Content, Research, Developer, Assistant — used here for Training Club operations
- **Day-1 skills tuned for Training Club operators:** weekly retention review, weekly content batch, race-anchored block builder, member check-in drafter
- **Vault scaffold for Training Club ops:** Members/, Coaches/, Programming/, Events/ folders pre-built with the right starter templates
- **HYROX brand context** baked into the brand voice layer — race calendar awareness, programming vocabulary, member language
- **Integrations roadmap** for Flexybox, Mindbody, Glofox (the booking platforms most Training Club operators actually use)

Free to install for your own use. Built by the team behind this kit. Given away because the world is better when more Training Club operators have a real AI partner instead of trying to bolt ChatGPT onto their workflow.

---

## What you walk away with

A typical day inside this AI:

**Monday 06:30:** AI fires your morning brief — today's classes, who's attending, members flagged amber/red, content scheduled, open threads. Telegram delivery, you read it on the way to the club.

**Wednesday afternoon, 20 min between classes:** *"Draft 3 Instagram posts about the upcoming Copenhagen race."* AI knows your voice, knows the race date, drafts on your phone, you review and approve.

**Friday evening:** Newsletter routine fires. Pulls this week's race results from members signed up to events, member wins, class highlights — drafts the issue in your voice. Ready for review Saturday morning.

**Sunday night 19:00:** Weekly retention review fires. Traffic-light dashboard — who's at risk, who's on a roll, suggested coach check-ins for the week ahead.

**Anytime mid-day:** *"Add Anders to amber for the week — he seemed off after Wyrm today."* AI logs it. Next time you ask about Anders, that context is there.

You never open a terminal. You talk to your AI like you'd talk to a chief of staff.

---

## How to install

**Prerequisites:**

Three obvious ones plus two that aren't obvious — but the two non-obvious ones are **half the magic**. Don't skip them.

**The obvious three:**

1. **A Mac** running macOS 14 or later
2. **A Claude subscription** (any tier — Pro covers it)
3. **Claude Code Desktop** installed → [download here](https://claude.com/code)

**The two that turn the AI from chatbot into agent:**

4. **"Computer use" turned ON inside Claude Code Desktop.** Toggle is in **Settings → Capabilities** (look for *"Computer use"* or *"Control my computer"*). Grant Screen Recording + Accessibility permissions when prompted.

5. **The Claude Chrome extension** installed + paired. [Get it from the Chrome Web Store](https://chromewebstore.google.com/search/Claude). After install, click the extension icon once in Chrome so it pairs with Claude Code.

**Why those two matter — it's the aha-moment, not just smoothness.**

A chatbot says *"open System Settings and turn on iCloud Drive."* A partner **opens System Settings for you, takes a screenshot, points at the toggle.** A chatbot says *"go to granola.ai and create an account."* A partner **opens the page, fills the form, navigates the onboarding.** The first time your AI does that during this install — and there will be a dozen moments — is when the partnership stops feeling like a metaphor.

This matters even more for Training Club ops: club CRMs, member portals, your scheduling tool, ClassPass, Stripe — they're all in the browser. An agent that can navigate them with you is on a different planet from one that can't.

Without computer use + Chrome extension: you still get a working Partner AI, but every visual moment becomes *"tell me what you see"* and every web flow becomes *"navigate here, click this, copy that."* Smart chatbot. Not an agent.

If you genuinely can't enable them (corporate-locked Mac, no Chrome), the install will still complete — just in manual mode. But if you can enable them, do.

**Plus: connectors (the agent's reach).** During install your AI will offer to connect 4 starter apps in ~5 minutes: **Gmail, Calendar (Google or Apple), Drive (Google or iCloud), Apple Notes.** Day-one wins for Training Club operators: *"what trial inquiries came in today?"*, *"what's the class schedule for tomorrow?"*, *"pull up the waiver template"*, *"add a note from the coach sync."* Skip any you don't use. Multi-account operators (personal + club Gmail) — your AI will help you pick the right account at OAuth time so you don't connect the wrong inbox.

**The install:**

1. Open Claude Code Desktop
2. Paste the prompt below
3. Hit Enter
4. Answer the questions your new AI asks you (~30 min total — a bit longer than the Personal version because of the Training Club overlay)

### The install prompt

```
You're about to install the Partner AI Kit (Training Clubs) for me.
I'm not a developer. I run a Training Club and want an AI partner
built for my operation.

Please:
1. Fetch the live installer from
   https://raw.githubusercontent.com/DanJoachimn/Partner-Ai-Kit-Training-Club/main/INSTALL.md
2. Read it carefully — it has the full install playbook. The Training Club version
   layers on top of the Personal kit, so you'll install both.
3. BEFORE installing ANYTHING, do a security audit of BOTH repos (Personal
   foundation + Training Club overlay). Clone each to a sandbox folder, read through
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

## Your four digital employees

Your AI ships with **four digital employees** — specialists your orchestrator hands tasks to when the work fits their lane. Same four for everyone; you'll add new ones (or teach the existing four new tricks) as real use cases emerge from running your Training Club.

Think of it like hiring four people, each for a different domain. You talk to the chief of staff (the orchestrator). The chief of staff dispatches the right person.

### Content
Video editing, writing, design. Drafts in your voice — social posts, newsletter copy, race-week comms, member-win celebrations, inquiry replies. Reads your Brand/Voice guide before every draft.

### Research
Deep-dives, sources, fact-checking. Pulls together background on members, suppliers, competing clubs, race results, HYROX news. Hands you the synthesis, not the raw search dump.

### Developer
Anything with code. Scripts to scrape your booking platform, automations to wire up new tools, custom integrations when no off-the-shelf option exists. Quiet most days; useful when needed.

### Assistant
Daily admin — emails, calendar, scheduling, follow-ups, meeting-notes cleanup, action-item extraction. Reduces your mental load instead of adding to it.

**Teaching a digital employee a new task = adding a new "skill."** Once you've shown one of them how to handle something three weeks in a row, the AI will offer to make it a one-button task going forward. That's how the team gets sharper over time — they learn your operation by doing it with you.

---

## The Day-1 skills (more grow over time)

Four skills come pre-installed. Each one is built specifically for Training Club operators:

| Skill | Trigger | What it does |
|---|---|---|
| `morning-brief` | Auto 06:30 daily | Today's classes + attendees + members flagged + content scheduled + open threads |
| `weekly-retention-review` | Auto Sunday 19:00 | Traffic-light dashboard, top members at risk, coach check-in suggestions |
| `weekly-content-batch` | Auto Sunday 20:00 OR manual | Drafts 7 days of social posts for review |
| `block-builder` | Manual: *"build me a 4-week block ending at HYROX Copenhagen"* | Race-anchored training block with scaling options |
| `member-checkin-draft` | Auto when member hits amber, or manual: *"draft a check-in for Anders"* | Personalized message in your club's voice, ready to send |

More skills get built **as you notice patterns in your work** — the kit's proactive opportunity-spotting (built into the kick-off and wrap-up flows) surfaces *"hey, you've done this manually 3 weeks running, want me to turn it into a skill?"*

---

## The vault scaffold (Training Club-flavored)

On install, your vault gets these Training Club-specific folders:

```
~/Documents/[your-ai-name]/vault/
├── Members/         ← one file per member, with traffic-light state + recent context
├── Coaches/         ← your team
├── Programming/     ← workout blocks, scaling library, benchmark sessions
├── Events/          ← race calendar, internal comps, community events
└── (plus the Personal kit defaults: Brand/, Projects/, Notes/, Memory/, etc.)
```

The `_context/` layer gets Training Club-aware starter templates — your brand voice doc has prompts like *"how do you talk about HYROX races vs general fitness?"* baked in.

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

- **Flexybox / Mindbody / Glofox MCP integrations** — Coming Q3 2026. Currently the Assistant subagent can read your data if you paste/export it; direct API hookup is the next big unlock.
- **HYROX race calendar feed** — Manual entry for now. Live feed planned once HYROX exposes one.
- **Native dashboard UI** — The kit lives entirely inside Claude Code Desktop. A custom dashboard ("Pacer cockpit") is on the roadmap but not blocking — the chat interface is already the primary way operators use it.

---

## License

Source-available. You can install, modify, and use this kit for your own needs (personal or your own Training Club). You can't repackage it for sale, host it as a service for others, or distribute a competing kit derived from it.

Full terms in [LICENSE](./LICENSE). For commercial licensing inquiries: open an issue on [GitHub](https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club/issues) and I'll be in touch.

---

## Stay in touch — The ROXIE Stacked

One optional thing before we finish.

The kit gets you running. **The ROXIE Stacked** keeps you current.

This is the Substack + community for Training Club operators running modern operations. It's where the "cut through the noise" promise compounds: new skill releases land here first, real reports from other operators, tactical playbooks, what flopped, what you can copy.

- **Free Substack** — first word when new Training Club skills ship to your kit, tactical posts, occasional deep-dives → [https://theroxiestacked.substack.com](https://theroxiestacked.substack.com)
- **Paid community** *(coming soon, yearly billing)* — monthly office hours, early skill drops, member-only operator threads, shared playbooks across clubs
- **1:1 install + tuning** *(coming soon, capped volume)* — for the rare Training Club that wants me to install + tune the kit for them rather than self-installing

Full details in [`STAY_IN_TOUCH.md`](./STAY_IN_TOUCH.md).

No email required to install. No tracking. The campfire's there if you want it.

---

## Help, feedback, bug reports

Open a [GitHub issue](https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club/issues).

Or tell your AI about a bug — it can often diagnose and propose a fix. If the fix is useful for everyone, it can open a PR back to this repo.

---

## Who built this

I work with Training Clubs on retention, content, and AI-augmented operations. This kit is the install foundation I use for every client engagement — given away free because the Training Club space is too small for paywalled tooling and too big for everyone to reinvent the same wheels.

If you want help setting yours up beyond what your AI can do, or you want a custom-built version with your specific integrations + content workflows, [open an issue on GitHub](https://github.com/DanJoachimn/Partner-Ai-Kit-Training-Club/issues) and we'll find a way to talk.

---

*Built with [Claude Code](https://claude.com/code). The whole kit was designed in conversation with an AI partner. Recursion is the point.*
