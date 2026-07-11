# CLAUDE.md — AI-103 Repo

Project context and invariants for Claude Code sessions. Read this first, then `STATE.md`, then the latest session log.

## What this repo is

Study and build repo for **Exam AI-103 / Microsoft Certified: Azure AI Apps and Agents Developer Associate**, targeting a **mid-September 2026** exam sit. The build spine is the capstone:

> **ADT Delivery Agent** on Azure AI Foundry — a Foundry agent that ingests project governance docs (RAID logs, PIDs, status reports) into Azure AI Search, answers grounded questions over them, calls a tool to read/write Jira issues, runs content safety, and is instrumented with evaluations and tracing.

The capstone doubles as **Pilot P1** for the 2028 QUT Masters capstone (ADSA) — see `ADSA-capstone-concept-brief.md`. Evidence discipline matters: eval results, cost data, and session logs are future research citations, not just hygiene.

## Owner context

- Pradeep (Prad) De Silva — Delivery Lead transitioning to AI engineering; PMP; strong Jira/Confluence/delivery domain knowledge; Python moderate (Flask/MySQL background), TypeScript strict via initiative-sync
- Study budget: **8–10 hrs/week**. Tue/Thu evenings = reading; Saturday = lab/build; Sunday = practice questions
- Related repos: `initiative-sync` (Forge, TypeScript), ADT Jira project on `pradeep-de-silva.atlassian.net`

## Invariants (do not violate)

1. **Subscriptions:** QUT Azure for Students subscription = disposable compute for labs. **Nothing precious lives there.** Personal MSA owns the exam booking, GitHub portfolio, and (from ~Week 5) the personal free-account subscription for the capstone demo. Never book or register anything durable under `n12850322@qut.edu.au`.
2. **No client data. Ever.** All governance docs in the corpus are synthetic, modelled on artefact *types* from career experience. If a doc looks real, stop and ask.
3. **Model discipline:** default to the smallest current-generation model (gpt-5-mini / gpt-5-nano class). No frontier models except a final capstone demo, if at all. Check the [model retirement schedule](https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/model-retirement-schedule) before building on any model; never build on a model retiring before **Nov 2026**.
4. **Cost discipline:** budget alert at $20 must exist before any deployment. Deploy at minimum TPM (1K) unless a lab requires more. `az group delete` at end of every lab session unless STATE.md says otherwise. One resource group per learning path.
5. **IaC or it didn't happen:** capstone infrastructure lives as Bicep or `az` CLI scripts in `/infra`. The environment must be reproducible in any subscription with one command.
6. **Propose–gate–execute:** the agent never writes to Jira without an explicit human gate. Every write proposal is logged before it is gated.
7. **Audit log is append-only** (`/data/audit/*.jsonl`). Never rewrite history; it's the research dataset.
8. **Evidence discipline:** every lab and pilot milestone records at least one measured metric (groundedness, cost, latency, accept/reject rate — however crude) in `/evals/results/`.
9. **Session continuity:** every session ends by updating `STATE.md` and appending a session log to `/docs/sessions/`. Significant decisions become ADRs in `/docs/adr/` (`ADR-NNN-title.md`).
10. **Exam scope is the tiebreaker:** when choosing between two approaches, prefer the one the AI-103 study guide tests. This is a cert repo first, product repo second.

## Repo layout (target)

```
/agent           Python — Foundry agent, tools, gating logic
/infra           Bicep / az CLI — reproducible environment
/corpus          Synthetic governance docs (RAID, PID, status) + generation scripts
/evals           Evaluation harness + /results
/data/audit      Append-only JSONL action log
/docs/adr        Architecture decision records
/docs/sessions   Session logs (YYYY-MM-DD-topic.md)
CLAUDE.md  STATE.md  adsa-notebook.md  AI-103 Study Plan.md  ADSA-capstone-concept-brief.md
```

## Tech defaults

- Python 3.12+, venv, `azure-ai-projects` / `azure-ai-agents` SDKs; type hints everywhere
- Auth: managed identity / keyless wherever supported; API keys only where a lab forces it, never committed
- Atlassian: REST or MCP against the personal instance (cloud ID `6766f31f-291d-45d4-b797-ab98e0a9a7e6`), ADT project only
- Secrets via `.env` (gitignored) locally; Key Vault when deployed
- Naming: `rg-ai103-<path>` for resource groups; `adt-` prefix for capstone resources

## Session workflow

1. Read `STATE.md` → confirm current phase, open threads, and any standing "don't delete" flags
2. Do the work; keep changes small and runnable
3. Before ending: update `STATE.md`, write session log, raise ADR if a decision was made, note any metric captured
4. If a study-plan week boundary passed, tick progress in `AI-103 Study Plan.md`
5. Monthly (or on pilot milestone): prompt Prad to add an `adsa-notebook.md` entry

## Known traps (learned so far)

- Foundry provisions S0 by default; F0 free tiers only exist on standalone Cognitive Services resources created directly
- Student-subscription quota is tiny for new frontier models — lower TPM in the deploy dialog before assuming quota is absent
- gpt-4o family is deprecated/retiring through 2026 — do not use despite available quota
- OnVUE proctoring does not support Linux; exam will be sat at a Brisbane Pearson VUE test centre