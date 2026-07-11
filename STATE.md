# STATE.md — AI-103 Repo

> Single source of truth for "where are we." Updated at the end of every session. Newest information wins; history lives in `/docs/sessions/`.

**Last updated:** 2026-07-12 (repo initialisation)
**Current phase:** Week 0 — Pre-start setup
**Exam target:** mid-September 2026 (NOT YET BOOKED)
**Next session should:** complete Week 0 checklist below

---

## Now / Next / Later

**NOW (Week 0 — before study starts)**
- [ ] Read official study guide (https://aka.ms/AI103-StudyGuide) — note current domain weights here when read
- [ ] Confirm AI-103 GA status and price at booking time
- [ ] Book exam for ~week of 14 Sep 2026 at a **Brisbane Pearson VUE test centre**, using **personal MSA** (not QUT account)
- [ ] Check Microsoft Learn events page for free/discounted voucher options before paying
- [ ] Azure for Students subscription active; **set $20 budget alert** (Invariant #4 — blocks all deployments until done)
- [ ] Try the exam sandbox once (interface familiarity): linked from certification page
- [ ] Scaffold repo layout per CLAUDE.md
- [ ] Email QUT course coordinator re: IFQ735 industry-partner requirement (ADSA brief §8, due end-2026 — not urgent, but cheap to do now)

**NEXT (Week 1 — Python + Foundry orientation)**
- [ ] Python refresh if needed (async/await, typing, venv)
- [ ] MS Learn: Develop AI apps with Azure AI Foundry — intro modules
- [ ] Create Foundry project; deploy **smallest current-gen model** (gpt-5-mini/nano class, 1K TPM); one successful SDK call from Python
- [ ] Record first cost datapoint in /evals/results/

**LATER (headline milestones)**
- Week 2: Plan & manage domain; switch to managed identity; content safety filter
- Weeks 3–5: RAG (AI Search) → Agents (Foundry Agent Service, Jira tool) → hardening (evals, tracing) — capstone core
- Week 5–6: stand up **personal-MSA free-account subscription**; capstone demo environment lives there via /infra IaC
- Week 6: vision / text analysis / info extraction labs (standalone F0 resources, NOT via Foundry)
- Week 7: timed practice exam(s); wrong-answer log; re-lab weakest two areas (target 75%+)
- Week 8: mixed-domain drills; rehearse in-exam Microsoft Learn search; sit exam
- On P1 ship: create first adsa-notebook.md entry; update ADSA brief review log

---

## Capstone build state — ADT Delivery Agent

| Component | Status | Notes |
|---|---|---|
| Foundry project + model deployment | not started | |
| Synthetic corpus (RAID/PID/status) | not started | Generation scripts in /corpus; no client data (Invariant #2) |
| AI Search index + grounding | not started | Free tier OK for basic RAG; brief paid Basic for semantic-ranking + managed-identity labs |
| Jira tool (read/write, gated) | not started | ADT project only; propose–gate–execute (Invariant #6) |
| Content safety | not started | |
| Evaluations + tracing | not started | Harness v0 = groundedness + action-precision |
| /infra IaC | not started | Must reproduce env in one command (Invariant #5) |

## Open threads & decisions pending

- Exact small-model choice — decide in Week 1 against live catalogue + retirement schedule → ADR-001
- Jira integration: REST vs MCP → decide Week 4 → ADR-002
- Practice assessment: official one not yet published (cert recently GA) — recheck certification page Week 6; fallback = reputable third-party sets, no dumps

## Standing flags

- Nothing marked "don't delete" yet — all resource groups are teardown-eligible
- QUT subscription: labs only. Personal subscription: capstone demo (from Week 5–6)

## Wrong-answer log

*(starts Week 7 — table: what I got wrong / why / doc page that fixes it)*

## Session log index

*(append one line per session: date — topic — link)*