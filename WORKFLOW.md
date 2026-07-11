# WORKFLOW.md — Running this repo with Claude Code

Practical instructions for coding, testing, and studying with Claude while keeping `CLAUDE.md`, `STATE.md`, `adsa-notebook.md`, and the study plan current. The md files only have value if they're true; this document is how they stay true.

---

## The one rule that makes everything work

**Every session ends with a state update.** Not most sessions — every session, even a 20-minute one. A stale STATE.md is worse than none, because the next session will trust it. The closing prompt (§4) does this in one step. If you only adopt one habit from this file, adopt that one.

---

## 1. File responsibilities at a glance

| File | Purpose | Updated by | When |
|---|---|---|---|
| `CLAUDE.md` | Invariants + project context. Claude Code reads it automatically at session start | **You** (Claude proposes, you approve) | Rarely — only when an invariant changes or a new trap is learned |
| `STATE.md` | Where we are right now: phase, NOW/NEXT/LATER, build status, open threads | **Claude**, at your instruction | End of every session |
| `/docs/sessions/YYYY-MM-DD-topic.md` | What happened in one session | **Claude** | End of every session |
| `/docs/adr/ADR-NNN-title.md` | One significant decision, its context and consequences | **Claude drafts, you approve** | When a decision is made (not after) |
| `adsa-notebook.md` | Research log for the 2028 capstone | **You** (Claude can draft) | Monthly + on pilot milestones |
| `AI-103 Study Plan.md` | The 8-week study spine with checkboxes | **Claude ticks, you verify** | At week boundaries |
| `ADSA-capstone-concept-brief.md` | Capstone positioning | **You** | On pilot ship + TP boundaries (append to review log) |

Division of labour in one line: **Claude maintains the operational files (STATE, sessions, ADR drafts); you own the judgement files (CLAUDE.md invariants, notebook, brief).**

## 2. Opening a session

Start every Claude Code session in the repo root. CLAUDE.md loads automatically. Then orient with:

```
Read STATE.md and the most recent session log. Confirm: current phase,
what "next session should" says, and any open threads or standing flags.
Then propose a plan for this session sized to [90 min / 3 hrs].
```

Why the size matters: your Saturday block is 3–4 hrs, weeknights ~1.5. Telling Claude the budget stops it proposing a plan you can't finish, which is the main cause of sessions ending without a state update.

**If Claude's summary of STATE.md doesn't match your memory, fix STATE.md first, before any work.** Divergence compounds.

## 3. During the session — coding and testing

These reinforce the CLAUDE.md invariants at the moments they're most easily violated:

- **Before any Azure deployment:** ask Claude to confirm the budget alert exists and state the model + TPM it intends to deploy, and check it against the retirement schedule. One sentence of prompt, saves real money: *"Before deploying, confirm invariants 3 and 4 are satisfied and tell me what you're about to create."*
- **Tests before fixes.** When something breaks, the habit is: *"Write a failing test that reproduces this, then fix it."* This keeps your test-authorship separation discipline intact and leaves evidence.
- **You run the destructive commands.** Let Claude propose `az group delete` or anything that touches the Jira ADT project; you execute or explicitly approve. This is propose–gate–execute applied to your own tooling — practise the pattern you're building.
- **Metric capture is part of "done."** A lab or feature isn't complete until at least one number lands in `/evals/results/` (cost of the session's API calls, a groundedness score, latency, accept/reject count — crude is fine). Prompt: *"Before we close this out, what metric did this session produce and where is it recorded?"*
- **When you disagree with Claude's approach,** say so and ask for the trade-off table rather than accepting or overriding silently. If the resolution is significant → ADR.

**Model selection habit (Claude Pro):** Opus for architecture sessions, ADR debates, and study-plan revisions; Sonnet for implementation and labs; Haiku for quick lookups. Starting an implementation session on Opus burns your allowance; starting an architecture session on Haiku burns your time.

## 4. Closing a session — the closing prompt

Paste this (or save it as a snippet / custom command):

```
Close out this session:
1. Update STATE.md — phase, NOW/NEXT/LATER, capstone build table, open
   threads, and set "Next session should:" to one concrete sentence.
2. Write /docs/sessions/YYYY-MM-DD-<topic>.md — what we did, what worked,
   what's unresolved, any metric captured.
3. If we made a significant decision, draft an ADR and show it to me
   before saving.
4. If a study-plan week boundary passed, tick the relevant items in
   "AI-103 Study Plan.md".
5. Tell me if anything from this session belongs in adsa-notebook.md,
   and draft the entry if so — but I will paste it in myself.
6. Remind me if any Azure resources are still running that should be
   torn down.
```

Point 5 is deliberate: Claude drafts notebook entries, but you commit them by hand. The notebook is your research voice for the thesis; keeping the final edit yours means you can honestly claim it in 2028.

## 5. What counts as an ADR

Write one when a decision is (a) hard to reverse, (b) has real alternatives you rejected, or (c) future-you will ask "why on earth did we do it this way?" Examples from this repo's known pipeline: model choice (ADR-001), REST vs MCP for Jira (ADR-002), corpus synthesis approach, eval harness design. Format: Context → Decision → Alternatives considered → Consequences. One page max. Sequential numbering, never reused.

Not an ADR: variable names, folder layout, which tutorial you followed.

## 6. Weekly and monthly rhythm

**Sunday (10 min, with the practice questions):**
- Skim STATE.md — is it still true? Tick study-plan progress for the week
- Wrong answers from practice → wrong-answer log in STATE.md (Week 7+)

**Monthly (10 min, first Saturday):**
- One `adsa-notebook.md` entry, even if it's a single PLATFORM-WATCH line. The ≥12-entries target in the brief's definition-of-ready assumes you never skip
- Glance at the brief's §8 risk table — anything change?

**On pilot ship (P1 in ~September):**
- Notebook entry (substantial one — what the pilot proved, what surprised you)
- Append to the brief's review log
- Tag the repo (`git tag p1-adt-agent`) so the evidence state is frozen and citable

## 7. Git hygiene that supports all this

- Commit at least once per session; the session log filename in the commit message links them (`feat: jira tool gating — see docs/sessions/2026-08-02-jira-gate.md`)
- `.env`, `/data/audit/` real logs if sensitive → gitignored; audit log *structure* and synthetic samples stay in
- STATE.md merge conflicts mean two sessions ran without syncing — resolve by re-reading both session logs, not by picking a side blindly

## 8. Failure modes to watch for (meta)

- **STATE.md drift** — sessions ending "just this once" without the closing prompt. Two skips and the file is fiction
- **CLAUDE.md bloat** — resist adding session detail to it; that's what session logs are for. CLAUDE.md should stay readable in one screen-scroll
- **Notebook procrastination** — "I'll write a proper entry later" = no entry. A two-line entry beats a deferred perfect one
- **Claude over-trust on Azure specifics** — model names, quotas, and SDK surfaces change monthly; when Claude states a current fact about Azure from memory, ask it to verify against live docs before you build on it. (This conversation already caught gpt-4o quota looking healthy on a deprecated model.)