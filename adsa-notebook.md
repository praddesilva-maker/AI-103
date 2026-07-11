# ADSA Notebook — Running Research Log

> Raw material for the 2028 QUT capstone (IFQ735–IFQ736-2). Ten minutes a month, minimum; more on pilot milestones. Entries are append-only and dated. See `ADSA-capstone-concept-brief.md` §6 for what belongs here.
>
> **Entry types:** `FAILURE-MODE` · `DESIGN-LESSON` · `LIT` · `METRIC-IDEA` · `PLATFORM-WATCH`
>
> Anonymise anything from the day job. No client names, no identifiable programs.

---

## How this becomes the thesis

- `FAILURE-MODE` entries → problem-statement evidence and motivation chapter
- `DESIGN-LESSON` entries → preliminary-work chapter and ADR citations
- `LIT` entries → literature review (target ≥15 items by late 2027)
- `METRIC-IDEA` entries → evaluation-methodology chapter (RQ-D)
- `PLATFORM-WATCH` entries → the 2027 platform decision (ADR-001 of the capstone)

Definition-of-ready target (brief §9): **≥12 monthly entries and ≥15 LIT items by late 2027.**

---

## Entries

### 2026-07 — Notebook initialised

**PLATFORM-WATCH:** gpt-4o family deprecated on Azure Foundry mid-2026 (two versions retired 31 Mar, last retires 1 Oct 2026); documented migration path gpt-4.x → gpt-5.x family. Lesson for capstone: GA models now carry an 18-month retirement clock set at launch. Any system with a >12-month horizon must treat model choice as a rotating dependency, not a foundation — argues for a model-routing abstraction layer in ADSA. Source: MS Learn model-retirement docs.

**PLATFORM-WATCH:** "Azure AI Foundry" rebranding to "Microsoft Foundry" observed across MS Learn during 2026. Naming churn is itself evidence for keeping the capstone's architecture chapter platform-agnostic in its vocabulary (orchestrator/specialist/gate, not vendor product names).

**DESIGN-LESSON (pre-pilot, from planning):** Foundry does not inherit free-tier (F0) quotas from standalone Cognitive Services — platform consolidation traded away granular cost control. Relevant to ADSA's cost-governance argument (RQ-C adjacent): enterprise agent platforms may make cost attribution *harder*, not easier.

**METRIC-IDEA:** "Action-precision" — proportion of agent-proposed writes accepted unmodified by a qualified delivery professional at the gate. Complement with "edit distance" on modified proposals. Candidate primary metric for RQ-B.

*(next entry due: 2026-08)*

---

<!-- TEMPLATE — copy below for each new entry

### YYYY-MM — short title

**TYPE:** one or more entries. Keep each to 2–5 sentences: what was observed / read / decided, and why it matters for ADSA. LIT entries: citation + one-line relevance.

-->