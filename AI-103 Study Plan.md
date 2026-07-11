# AI-103 Study Plan — Developing AI Apps and Agents on Azure

**Target credential:** Microsoft Certified: Azure AI Apps and Agents Developer Associate
**Owner:** Prad
**Duration:** 8 weeks @ 8–10 hrs/week (~70 hrs)
**Suggested window:** Start mid-July 2026 → sit exam ~mid-September 2026

---

## 0. Before you start (Week 0 — 2 hrs)

- [ ] Open the **official study guide** on Microsoft Learn (`learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103`) and confirm:
  - Current **skills-measured weights** (this plan assumes the April 2026 outline — verify)
  - **GA vs beta status** — if still beta, exam is ~US$99 but scores are delayed; at GA it's ~US$165 with immediate scoring
- [ ] Create an Azure account. Set a **spend cap / budget alert** — you'll be deploying models and Search indexes.
- [ ] Check Microsoft Learn events page for **free/discounted exam vouchers** (Cloud Skills Challenges, Virtual Training Days) before paying.
- [ ] **Book the exam now** for ~week 9. A booked date is the single biggest driver of completion.

---

## The spine: one project, not a pile of modules

Everything below hangs off **one build**. Don't study modules in isolation.

> **Capstone: "ADT Delivery Agent" on Azure AI Foundry**
> A Foundry agent that ingests project governance docs (RAID logs, PIDs, status reports) into Azure AI Search, answers grounded questions over them, calls a tool to read/write Jira issues, runs content safety, and is instrumented with evaluations and tracing.

This is essentially **initiative-sync's architecture ported to Azure**. It covers the highest-weighted exam domains *and* becomes a portfolio artefact for the "Delivery Lead building AI agents for PMO/delivery" positioning. Two birds.

---

## Week 1 — Python + Foundry orientation (8 hrs)

Your agent instincts are strong; your Azure hands are not. This week is about closing the *environment* gap.

- Refresh Python: `async`/`await`, typing, virtualenvs, `pip`. If you're comfortable, skip to Foundry. (2 hrs)
- Microsoft Learn path: **Develop AI apps with Azure AI Foundry** — intro modules only. (3 hrs)
- Hands-on: create a Foundry project, deploy a chat model, call it from Python with the Foundry SDK (`azure-ai-projects`). Send one request. (3 hrs)

**Done when:** you have a Python script hitting your own deployed model.

---

## Week 2 — Plan and manage an Azure AI solution (~25–30% of exam) (10 hrs)

The domain people skip and then fail on. Your PM/governance background is an *advantage* here — lean in.

- Model and service selection: when Azure OpenAI vs AI Search vs Document Intelligence vs Content Understanding
- Deployment options, quota, tokens, cost estimation (you'll find this easy)
- **Identity and security:** managed identity, keyless auth, RBAC, private endpoints
- **Responsible AI:** content safety filters, provenance, risk metrics
- CI/CD and monitoring for AI workloads

**Hands-on:** switch your Week 1 script from API keys to **managed identity**. Add a content safety filter.

**PMO tie-in:** this domain maps almost 1:1 to ISO/IEC 42001 controls. Take notes — it's reusable commercially.

---

## Weeks 3–5 — Generative AI and agentic solutions (~30–35% — the big one) (30 hrs)

This is where the exam is won or lost. Budget three full weeks.

### Week 3 — Grounding and RAG
- Ingest documents into **Azure AI Search**: chunking, embeddings, hybrid + vector indexes
- Wire your Python app to the index; get grounded answers
- Add **evaluators**: groundedness, relevance, hallucination rate

### Week 4 — Agents
- **Foundry Agent Service**: agent definition, instructions, threads, tool calling, code interpreter
- **Microsoft Agent Framework** and multi-agent orchestration
- Agent memory and state

**Critical distinction the exam hammers:** know exactly when the answer is an **agent** (tool-calling, threaded conversation, code execution) vs **prompt flow** (versioned, evaluated, deployable pipeline) vs **AI Search** (retrieval over your own docs drives the answer). Scenarios will make two of them look plausible.

### Week 5 — Production hardening
- Prompt engineering and structured outputs
- Evaluations, tracing (OpenTelemetry), observability
- Guardrails, error analysis, failure modes

**Done when:** your ADT Delivery Agent runs end-to-end with a Jira tool call, grounded retrieval, safety filters, and tracing enabled.

---

## Week 6 — The "other" domains (10 hrs)

Lower weight, but easy marks — don't donate them.

- **Computer vision:** image analysis, OCR, custom vision basics
- **Text analysis:** sentiment, entities, key phrases, PII detection, language detection
- **Information extraction:** Document Intelligence vs Content Understanding — *when to use which* is directly tested

**Hands-on:** extract structured data from a scanned PDF (use an old invoice or a status report). One lab is enough.

---

## Week 7 — Practice and gap-close (10 hrs)

- Take a **full-length timed practice exam**. Score it honestly.
- Microsoft's official practice assessment may not exist yet if AI-103 is recent — reputable third-party sets are fine, but **avoid dumps sites**; they teach wrong answers and are a cert-revocation risk.
- Log every wrong answer in a table: *what I got wrong / why / which doc page fixed it*
- Re-lab your two weakest areas. Reading won't fix them; the portal will.

**Target:** consistently 75%+ before you sit it.

---

## Week 8 — Final prep (6 hrs)

- Mixed-domain question sets (the exam context-switches; practice that)
- Rehearse the question routine: identify the goal → underline the constraint → identify the layer → choose the least risky option
- **You get Microsoft Learn access inside the exam** on associate-level exams. Practice searching Learn *fast* — it's near-useless if you haven't rehearsed it.
- Skim your wrong-answer log. Sleep.

**Exam day:** 120 minutes, ~40–60 questions, pass at 700/1000, scenario-heavy.

---

## Weekly rhythm that actually works

| | |
|---|---|
| **Tue / Thu evenings** | 1.5 hrs — Microsoft Learn modules + reading |
| **Saturday morning** | 3–4 hrs — hands-on lab / capstone build |
| **Sunday** | 1 hr — practice questions + wrong-answer log |

Protect the Saturday block. Hands-on Foundry time is the limiting factor across every candidate profile — not material consumed.

---

## Free resources (all you need)

- **Microsoft Learn** — official study guide + the AI-103 learning paths (free, and the exam is written from these)
- **Azure AI Foundry docs** — model deployment, agents, evaluations
- **Microsoft Learn Sandbox** — get familiar with the exam UI and item types
- **azure-ai-projects / azure-ai-agents Python SDK samples** on GitHub
- Microsoft Learn events page — free voucher hunting

Skip paid bootcamps. Spend the money on Azure consumption instead — that's the constraint.

---

## Risks to manage

| Risk | Mitigation |
|---|---|
| Exam still in beta → delayed score | Accept it; the credential is the same. Or wait for GA. |
| Skills outline changes (early lifecycle cert) | Re-check the Learn study guide at Week 4 |
| Azure spend blows out | Budget alert + delete Search indexes and deployments between labs |
| QUT semester load collides | 8 weeks is padded; you can compress Weeks 6–8 to 2 weeks if needed |
| Python rust | Add 2 weeks up front if Week 1 feels hard |

---

## Definition of done

- [ ] AI-103 passed
- [ ] ADT Delivery Agent repo public on GitHub with a README that reads like a case study
- [ ] LinkedIn + CV updated: *"Azure AI Apps and Agents Developer Associate — building agentic delivery tooling for PMO"*