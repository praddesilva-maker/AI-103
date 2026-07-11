# ADSA Capstone Concept Brief

**Agentic Delivery Support Agent — a governed multi-agent system for project delivery augmentation**

| | |
|---|---|
| **Author** | Pradeep De Silva |
| **Status** | Living document — review after every pilot ships and at each TP boundary |
| **Target** | QUT IFQ735 / IFQ736-1 / IFQ736-2 (Industry Capstone Pathway, 36cp), start 2028 |
| **Prerequisite** | INQ700 Introduction to Research (co-requisite permitted with IFQ735) |
| **Version** | 0.1 — July 2026 |
| **Review log** | *(append: date — what changed — why)* |

> **How to use this document:** This is not a project plan. It is a positioning instrument. Between now and late 2027, every pilot you ship, every failure mode you observe, and every paper you read gets logged here. In late 2027, the Phase 1 proposal is written *from* this document. If the brief is current, the proposal is a fill-in-the-blanks exercise.

---

## 1. Problem statement

Enterprise project delivery generates large volumes of structured and semi-structured artefacts — work item hierarchies, RAID logs, status reports, handover checklists, governance minutes — that decay faster than delivery teams can maintain them. The observable failure modes are consistent across organisations and sectors:

- **Thin work items:** Jira issues lacking acceptance criteria, context, or traceability, forcing rework and clarification loops.
- **RAID drift:** risk and dependency registers that are populated at kick-off and stale within weeks, so governance forums review fiction.
- **Handover gaps:** service transition to BAU with undocumented tribal knowledge, discovered only at incident time.
- **Status reporting theatre:** executive narratives produced by manual aggregation, lagging reality by a reporting cycle and filtered through optimism bias.
- **Dependency blindness:** cross-team sequencing decisions made without a current view of upstream/downstream state.

These failure modes are *observed first-hand* across 13+ years of delivery roles in Australian financial services (Westpac, CBA, Suncorp, Sunsuper/ART, QSuper), Queensland Government (Justice, Housing), and retail transformation (Super Retail Group, Flight Centre). They persist despite mature tooling (Jira, Confluence) because the constraint is not tooling — it is the sustained human attention required to keep delivery artefacts truthful.

**Premise:** LLM-based agents can supply that sustained attention — but only inside a governance envelope that keeps a human accountable for every consequential action. Whether such a system measurably improves delivery outcomes, and at what cost and risk, is an open empirical question. That question is the capstone.

## 2. Candidate research questions

*(Select and sharpen ONE primary question in the 2027 proposal; others become sub-questions or future work. All follow the pattern: capability → measurement → governance.)*

- **RQ-A (effectiveness):** To what extent can a governed multi-agent system improve the completeness and currency of delivery artefacts (work items, RAID logs, status narratives) compared with manual PMO practice, measured against a defined quality rubric?
- **RQ-B (trust & oversight):** What human-in-the-loop gating design achieves acceptable action-precision (agent-proposed changes accepted by a qualified delivery professional) while preserving throughput gains? Where is the accept/reject/edit equilibrium?
- **RQ-C (governance):** Can an agentic delivery system be operated demonstrably within an ISO/IEC 42001-aligned AI management envelope, and what controls are load-bearing versus ceremonial?
- **RQ-D (evaluation methodology):** What evaluation harness (groundedness, hallucination rate, action-precision, artefact-quality delta) is sufficient to make defensible claims about agent performance in PMO contexts?

**Selection heuristic for 2027:** RQ-A is the headline; RQ-B and RQ-D supply the methodology chapters; RQ-C is the differentiator no other student in the cohort can write credibly. A viable thesis = RQ-A primary + RQ-B/RQ-D as instruments + RQ-C as a dedicated chapter.

## 3. Why this author (grounding in professional experience)

| ADSA capability | Career evidence |
|---|---|
| RAID analysis and risk surfacing | Risk management practice; data & reporting risk management (SRG HRCP) |
| Dependency & sequencing analysis | Owned integration sequencing and dependency management (SRG Customer X) |
| Executive status narrative generation | UC3 prototype; status reporting across FS and Gov programs |
| Issue enrichment & backlog hygiene | Backlog management; handover gap identification and closure via Jira (HRCP) |
| Delivery health / maturity assessment | Team maturity assessments (Flight Centre, SRG DTOM transformation) |
| Service transition & handover checking | Owned BAU handover, documentation standards, governance processes (HRCP) |
| Governance cadence support | Embedded governance forums, DoD traceability, delivery controls (Customer X) |

This mapping is the capstone's authenticity claim: the agent skills are not speculative — they are a codification of manual practices the author has performed and coached in enterprise settings.

## 4. Architectural commitments (durable) vs. deferred decisions (2027)

### Durable — patterns that survive platform churn

1. **Propose–gate–execute.** Agents never write to systems of record without an explicit human gate. Every proposal carries provenance (what was retrieved, what was inferred).
2. **Orchestrator + specialist agents.** A routing agent delegates to narrow specialists (RAID Analyst, Issue Enricher, Narrative Writer, Handover Auditor, Maturity Assessor), each with scoped tools and scoped knowledge. No omniscient mega-agent.
3. **Three-layer knowledge model:**
   - *Methodology corpus* (static, curated): PMBOK-style practice, SAFe/Scrum guidance, author's coaching playbooks → embedded RAG.
   - *Organisational corpus* (synthetic, modelled on real artefact types): PIDs, RAID logs, status reports, handover checklists → embedded RAG. **Never real client data.**
   - *Live project state*: Jira/Confluence via API/MCP → retrieval-at-runtime, not embedding. The distinction between layers 2 and 3 is a design-chapter argument in its own right.
4. **Append-only audit log** (JSONL or equivalent) of every agent action, proposal, gate decision, and outcome. Doubles as the research dataset.
5. **Evaluation harness as a first-class component**, not a post-hoc test: groundedness, hallucination rate, action-precision, artefact-quality delta against rubric.
6. **Infrastructure as code.** Entire environment reproducible from the repo in any subscription. (Also insulates against the tenant-portability problem — see §8 risks.)

### Deferred to the 2027 proposal — record each as an ADR when decided

- Platform and agent framework (working default: **Azure Foundry**, aligned with AI-103 and employer stack — but decide against the 2027 landscape, not the 2026 one)
- Model selection and routing strategy (small models for classification/extraction; larger for narrative synthesis)
- Orchestration pattern specifics (supervisor vs. graph vs. event-driven)
- MCP vs. native connectors for Atlassian integration
- Evaluation baselines (which human-produced artefacts constitute the control set)
- Synthetic data generation methodology for the organisational corpus

## 5. Pilot roadmap (2026–2027) — evidence-generating builds

| # | Pilot | Window | What it proves | Evidence to keep |
|---|---|---|---|---|
| P1 | **ADT Delivery Agent** (AI-103 capstone): Foundry agent, AI Search grounding over governance docs, Jira tool call, content safety, tracing | Jul–Sep 2026 | Single-agent RAG + tool-use viability on Azure; evaluation harness v0 | Repo, eval results, session logs, cost data |
| P2 | **initiative-sync** maturation: Forge app, Jira↔Confluence bidirectional sync | Ongoing 2026 | Deep Atlassian data-model fluency; sync-conflict handling; TypeScript/Forge production discipline | Repo, ADRs, STATE.md history |
| P3 | **UC1 — Spec→Jira issue drafts** | 2026 H2 | Structured extraction quality; propose-gate-execute v1 | Accept/reject/edit rates per proposal |
| P4 | **UC2 — Issue enrichment from Confluence/SharePoint** | 2027 H1 | Multi-source retrieval; layered knowledge model v1 | Before/after artefact quality samples |
| P5 | **UC3 — Executive timeline narratives from live Jira** | 2027 H1–H2 | Narrative synthesis; hallucination measurement on generated claims | Groundedness scores; stakeholder feedback |
| P6 | *(Optional)* Cross-platform comparison (Bedrock or self-hosted) | 2027 H2 | Platform-independence of the patterns; cost/quality trade-off data | Comparison matrix |

**Rule:** small, complete pilots. Do not build full-vision ADSA before 2028 — it competes for the same 8–10 weekly hours as AI-103, advanced units, and initiative-sync, and would need rebuilding anyway. Synthesis is the capstone's job.

## 6. The ADSA notebook (running research log)

Maintain `adsa-notebook.md` in the repo. Ten minutes a month, minimum. Log:

- **Failure modes observed** — in pilots *and* in day-job delivery (anonymised): what broke, why, what a competent agent would have needed to catch it
- **Design lessons** — anything that changed an ADR or should have
- **Literature** — papers/posts on agentic systems, HITL patterns, LLM evaluation, AI governance; one-line relevance note each
- **Metric ideas** — candidate measures for the evaluation harness
- **Platform watch** — significant shifts in Foundry/Bedrock/agent frameworks that affect the deferred decisions

This notebook becomes the raw material for the literature review and the "preliminary work" chapter.

## 7. Governance & responsible AI (the differentiator chapter)

- **ISO/IEC 42001:2023** mapping: which controls the propose-gate-execute pattern, audit log, and evaluation harness satisfy; which require additional mechanism; which prove ceremonial (an honest finding either way is publishable)
- **Content safety** filters on all generation paths
- **Data ethics:** synthetic organisational corpus only; no client data ever; document the synthesis methodology
- **Accountability model:** the human at the gate owns the action; the agent owns the proposal; the audit log proves which was which
- Position explicitly against the capstone's likely cohort norm ("RAG chatbot over documents") — ADSA's claim is that *governed agency*, not retrieval, is the hard and interesting problem in enterprise delivery contexts

## 8. Risks and open questions

| Risk / open question | Mitigation / action | Owner-by-date |
|---|---|---|
| **Industry partner requirement unknown** — does IFQ735 need a sponsoring organisation? | Email course coordinator; check unit outline. If sponsor required: employer is the natural candidate — plant the conversation in 2027 *after* AI-103 pass + working demo | **Resolve by end 2026** |
| Platform churn invalidates early architecture | Defer platform decisions to 2027 proposal; keep patterns platform-agnostic; IaC everything | Ongoing |
| QUT tenant subscription loss at graduation | Nothing precious lives in QUT Azure; personal MSA for exam booking; portfolio in personal GitHub; IaC for reproducibility | Standing rule |
| Scope creep toward full ADSA build pre-2028 | §5 rule: small complete pilots only | Standing rule |
| Time contention (AI-103, advanced units, initiative-sync, work, family) | Capstone positioning costs ≤10 min/month (notebook) until proposal drafting in late 2027 | Standing rule |
| Research framing weak (build without measurement) | Every pilot ships with at least one measured metric, however crude; INQ700 concepts applied early | Per pilot |
| Synthetic corpus realism questioned by examiners | Document generation methodology; ground artefact templates in real (anonymised) structures from career experience | P4 onward |
| 2028 model capabilities make some agent skills trivial | Good problem; shifts research weight toward RQ-B/RQ-C (oversight and governance age well) | Reassess at proposal |

## 9. Definition of ready (for the late-2027 proposal)

The Phase 1 proposal can be written when all of the following are true:

- [ ] Industry-partner question answered; sponsor secured if required
- [ ] ≥3 pilots shipped with kept evidence (repos, eval data, accept/reject rates)
- [ ] ADSA notebook contains ≥12 monthly entries and ≥15 literature items
- [ ] One primary RQ selected and sharpened; evaluation approach sketched
- [ ] Platform decision made against the 2027 landscape and recorded as ADR-001
- [ ] AI-103 certification held (credibility for sponsor conversation and proposal)
- [ ] Supervisor conversation initiated with QUT (bring this brief)

---

*Companion artefacts: `AI-103-study-plan.md` (2026 study spine) · `adsa-notebook.md` (research log) · `CLAUDE.md` / `STATE.md` (session continuity) · `WORKFLOW.md` (how to run sessions) · ADT Jira project (pilot tracking)*