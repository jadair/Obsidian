# Tool Boundaries

Three tools, three distinct jobs. The rule that keeps this from turning back into tool-switching fatigue: **each piece of information has exactly one home**, and every other tool only *links* to it.

| Tool | Job | What lives here |
|---|---|---|
| **Obsidian** | Think and write | Notes, requirements, decisions, meetings, stakeholder context, deliverable descriptions |
| **GitHub Issues** | Track code work | Bugs, features, PRs — anything with a commit attached to it |
| **JIRA** | Roadmap and workload, at the project level only | One epic per active project in [[04 Projects/Home|04 Projects]] — nothing more granular |

If you're ever unsure where to put something, ask: *is this something I'm figuring out or deciding (Obsidian), code that needs to ship (GitHub), or a milestone someone above you needs visibility into (JIRA)?*

## The Flow

```
Obsidian note (requirement / decision / stakeholder ask)
        │
        ├── becomes engineering work ──────────► GitHub Issue
        │                                             │
        └── is a milestone / deliverable              │ (synced automatically
              worth tracking at a glance ──► JIRA Epic ◄─┘  once GitHub-JIRA
                                                            integration is set up)
```

- **Obsidian → GitHub Issue**: when a requirement or bug becomes real engineering work, create the GitHub Issue from the relevant project note and paste the issue URL back into that note. Don't duplicate the requirement text into the issue body beyond a summary — link to the Obsidian note for full context.
- **GitHub Issue → JIRA**: once the GitHub-JIRA integration is set up (see below), issues linked to a JIRA epic show their status automatically in JIRA. You should almost never need to open JIRA to update a status by hand.
- **Obsidian → JIRA epic (direct)**: for deliverables/milestones that aren't code (a stakeholder-facing document, an event, a proposal deadline), create the JIRA epic directly and link it from the project dashboard's Roadmap section. These are the only JIRA items you create manually.

## What Never Happens

- No mirroring every GitHub Issue into JIRA by hand — that's the integration's job.
- No writing full requirements docs inside JIRA or GitHub — they live in Obsidian; both other tools just link to them.
- No per-task JIRA tickets. If it's small enough to be a checklist item in a project note or a single GitHub Issue, it does not get its own epic.

## One-Time Setup: GitHub-JIRA Integration

Do this once so epics start reflecting issue status automatically instead of needing manual updates:

1. In JIRA, go to **Apps → Explore more apps** (or **Settings → Apps** depending on your JIRA edition) and install **"GitHub for Jira"** (Atlassian's official app).
2. Follow its prompt to connect your GitHub organization — this requires org admin approval on the GitHub side (you may need to ask whoever administers the CCI GitHub org if it's not you).
3. Once connected, any commit, branch, or PR whose message contains a JIRA issue key (e.g. `CCI-42`) will automatically link to that JIRA item and update its development status.
4. For issues that aren't naturally tied to a commit message convention, you can also manually link a GitHub Issue to a JIRA epic from the JIRA issue's "Link" menu — a one-time action per issue, not per status change.
5. Set the epic's key (e.g. `CCI-12`) as a habit in your branch names or PR titles going forward (`CCI-12-fix-login-bug`) so linkage happens automatically without extra steps.

Once this is live, your weekly review only needs to check JIRA's board/roadmap view — you won't need to manually reconcile GitHub Issue status against JIRA.

## Related

- [[00 Home/Roadmap|Roadmap]] — the holistic cross-project view this setup produces
- [[00 Home/Working Methodology|Working Methodology]]
- [[00 Home/Decisions|Decisions]]
- [[07 Templates/project-overview-template|Project Dashboard Template]]
