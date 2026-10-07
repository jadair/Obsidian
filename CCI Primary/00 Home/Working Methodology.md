# Working Methodology

How to operate this vault day to day. If you're ever unsure where something goes, capture it in [[01 Inbox/Capture|Capture]] and decide later — don't let indecision stop you from writing things down.

For the day-to-day mechanics, see the two notes this methodology is built on:

- [[00 Home/Daily Workflow|Daily Workflow]] — the start-of-day/during-the-day/end-of-week rhythm
- [[00 Home/Decisions|Decisions]] — how and when to make and record decisions

## Guiding Principles

This system leans on Peter Drucker's *The Effective Executive* for the underlying discipline, and on habits common among modern technology executives (Andy Grove, Jeff Bezos, and the broader "operating system" thinking popularized by leaders like Claire Hughes Johnson and Shreyas Doshi) for the day-to-day mechanics. Five ideas do most of the work:

1. **Know where your time actually goes.** Drucker's starting point isn't planning — it's recording. Effective executives track time before they manage it, because intention and actual usage diverge more than anyone expects. `02 Daily Notes` is this vault's time log: write down what you actually worked on, not what you meant to. Review it honestly, especially in the weekly review.
2. **Ask "what does the situation demand?" before "what do I want to do?"** Drucker frames contribution as the question "what can I contribute that will significantly affect the performance and results of the institution?" — not "what am I in the mood for." When triaging Inbox or planning the day, route by what the work actually requires (see the filing rules below), not by what feels most finished or most interesting.
3. **Build on strengths, staff and delegate around weaknesses.** Effective work comes from matching effort to strength — yours and other people's. When a task in a project or meeting's action items keeps stalling, that's a signal to reassign or restructure it rather than push through by willpower. Action items in meeting notes should name an owner, not just a task.
4. **Do first things first, and do one thing at a time.** Drucker's "concentration" principle: effective executives do the most important thing first, and only one important thing at a time — everything else is a distraction from it. This is why every daily note and project dashboard has a single `Priorities` section, not a flat task list — pick the one thing before you pick the ten things.
5. **Decisions are made deliberately, once, and are written down.** Drucker treats decision-making as a distinct, structured act — not something that happens implicitly in conversation. That's what the [[07 Templates/decision-record-template|decision record template]] is for. See [[00 Home/Decisions|Decisions]] for the full guidance on when and how to record one.

## Where Does This Go? Filing Rules

Ask these questions **in order**. Stop at the first one that gives you a clear answer.

### 1. Is this a record of a specific meeting?
If it has a date, attendees, and discussion/decisions from a real meeting (recurring 1:1, planning session, stakeholder call) → **`03 Meetings/<year>/YYYY-MM-DD — Meeting Name.md`**, using the meeting or one-on-one template.
- Even if the meeting was entirely about one project, the record still lives in `03 Meetings`, not inside the project folder. Link it *to* the project/area/people via frontmatter and `[[wikilinks]]` instead of filing it inside the project.
- A passing one-line mention of a meeting inside a daily note ("Meetings: Codefest Debrief") does **not** need to become a formal record unless there's enough substance (agenda, decisions, action items) to be worth its own note.

### 2. Is this tied to today specifically, or is it scratch/working notes for the day?
Priorities, quick notes, ideas, and ad hoc task tracking for *today* → **`02 Daily Notes/YYYY-MM-DD.md`**.
- Good fit: "talked to Jeff about X," a task you completed today, a quick idea that came up.
- Don't let daily notes become the permanent home for something that needs to survive past this week — if it's still relevant in a month, promote it (see below).

### 3. Does this belong to a project with a defined outcome and an end point?
If the work has a deliverable and a natural finish line (a feature, a launch, an event, a proposal) → **`04 Projects/<Project Name>/`**.
- If the project doesn't exist yet, create `04 Projects/<Project Name>/Home.md` from the [[07 Templates/project-overview-template|project dashboard template]] and add it to [[00 Home/Active Projects|Active Projects]] and `04 Projects/Home.md`.
- Only build out subfolders (`Source Material/`, `Working Notes/`, `Deliverables/`, `Reference/`) once the project has ~8-10+ notes or genuinely distinct note types that would otherwise blur together. Most projects should stay a flat folder.
- Decisions made within a project get their own record — see [[00 Home/Decisions|Decisions]] for where and when.
- Once a note describes work ready to be *done*, it may need to leave Obsidian entirely — see [[00 Home/Tool Boundaries|Tool Boundaries]] for when that means a GitHub Issue (code-level work) versus a JIRA epic (the project itself, or a non-code milestone).

### 4. Is this an ongoing responsibility with no finish line?
Recurring operational work you maintain indefinitely (not a one-time deliverable) → **`05 Areas/`**.
- If an area's work becomes time-bound (it gets a deadline and an end state), that piece should spin off into `04 Projects` and link back to the area.

### 5. Is this durable reference material, not tied to one project's timeline?
Books, articles, courses, frameworks, vendor docs, general how-tos, anything you'd want to reuse across multiple projects → **`06 Resources/`**.
- Use the `Type — Title — Detail` naming convention: `Book — Title — Author.md`, `Article — Title.md`, extended sensibly for videos, courses, podcasts, etc.
- If material is specific to one project and unlikely to ever matter elsewhere, keep it in that project's own reference material instead of Resources. If in doubt, put it in Resources and link from the project — don't duplicate it into both places.
- Something you're actively learning (a course, a tutorial, a new concept) → [[07 Templates/learning-note-template|learning note template]] in Resources.

### 6. None of the above are clear yet?
→ **`01 Inbox/`**. That's what it's for. Don't force a note into a category just to avoid using the Inbox — a wrong placement is more costly than a short Inbox stay.

## Quick Reference Table

| If it's...                                          | It goes in...                              |
| ----------------------------------------------------- | ------------------------------------------- |
| A dated meeting record                                | `03 Meetings/<year>/`                       |
| Today's priorities, quick notes, scratch work         | `02 Daily Notes/`                           |
| Work with a deliverable and an end point              | `04 Projects/<Project>/`                    |
| An ongoing responsibility with no end date             | `05 Areas/`                                 |
| Reusable reference material, books, courses, frameworks | `06 Resources/`                             |
| Not sure yet                                          | `01 Inbox/`                                 |

A decision, wherever it comes from, follows its own rule — see [[00 Home/Decisions|Decisions]].

## Habits That Keep This Working

- **Capture now, file later.** Speed of capture matters more than correct placement in the moment.
- **Link instead of duplicating.** If something relates to more than one project or area, link to it from both places rather than copying content.
- **Keep tags to workflow/type labels** (`#meeting`, `#decision`) — use links and frontmatter properties for people, projects, areas, and topics instead of tags.
- **Rename vague notes quickly** ("Untitled 2", "Notes") once you know what they actually are.
- **Archive, don't delete.** When a project or area's work is done or inactive, move the whole folder into `08 Archive` rather than leaving it to drift in `04 Projects`.
- **Process the Inbox on a cadence**, even if imperfectly — a slow trickle of filed notes beats a backlog that becomes too big to face.
- **One priority, not five.** A `Priorities` section with more than one or two items has stopped being a priority list. Move the rest to `Tasks`.
- **Name an owner on every action item.** "Someone should look at this" is not an action item. Match the task to whoever's strengths fit it, per Drucker's staffing principle — reassign stalled items instead of letting them sit.
- **Treat the calendar and daily notes as the source of truth for where time went**, not your memory of how the week felt. Use that record, not intuition, when reviewing whether priorities and actual work are still aligned.

## Related

- [[00 Home/Home|Home]]
- [[00 Home/Daily Workflow|Daily Workflow]]
- [[00 Home/Decisions|Decisions]]
- [[00 Home/Tool Boundaries|Tool Boundaries]]
- [[00 Home/Roadmap|Roadmap]]
- [[00 Home/Active Projects|Active Projects]]
- [[00 Home/Meeting Index|Meeting Index]]
