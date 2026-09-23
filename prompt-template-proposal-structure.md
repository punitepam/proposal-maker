# Prompt Template: Client Proposal Structure Generator

**Date:** 2026-09-22
**Author:** Punit Sharma — Delivery Manager, EPAM
**Project:** EPAM
**Model:** Chat GPT 5.2
**DIAL location:** my files/proposal maker
**Committed location:** 

---

## Purpose

Generates the full section-by-section structure of a client proposal — trends, gap analysis, prioritized scope, approach/commercial model, high-level architecture, capacity plan, and storyline — from a short context and objective brief, for use at the pre-sales/proposal-drafting stage of the delivery lifecycle.

---

## Variable Placeholders

| Placeholder | Description | Example value |
|---|---|---|
| `{{client_context}}` | Client name, industry, geography, and current-state summary (systems, pain points, constraints) | "FedEx CloudOps — logistics/transportation, North America. Current: fragmented Azure and AWS estates managed by three regional teams with no shared runbook or cost governance." |
| `{{project_objective}}` | The business outcome the client wants and the target completion horizon | "Consolidate CloudOps delivery under a single operating model within 6 months, reducing incident MTTR by 30% and cloud spend by 15%." |
| `{{scope_constraints}}` | Known boundaries: budget range, timeline, compliance/regulatory needs, vendor or platform preferences | "Budget: $1.2–1.6M annually. Must retain SOC 2 Type II compliance. Azure-first, AWS secondary. No new vendor onboarding before Q2." |
| `{{commercial_preference}}` | Preferred engagement/pricing model, if known | "Managed service with milestone-based transition pricing for the first 90 days." |
| `{{output_length}}` | Target length/depth of the generated structure | "Section headers + 2–3 bullet points per section, suitable for a 15-slide deck outline." |

---

## Output Format Instruction

Return a markdown document with H2 (`##`) section headers in this fixed order: Executive Summary, Current Trends, Gap Analysis, Prioritized Scope, Approach & Delivery Model, Commercial Model, High-Level Architecture, Capacity Plan, Storyline, Assumptions & Exclusions. Under each header, return 2–5 bullet points only — no narrative paragraphs, no restating the input verbatim. Do not include a preamble, closing summary, or any text before the first header or after the last section. If `{{output_length}}` requests a different depth, follow that instead of the 2–5 bullet default.

---

## Prompt Body

```
You are generating the structural outline for a client-facing delivery proposal. Do not write full prose paragraphs — produce a section-by-section skeleton that a delivery manager will expand into slides.

CONTEXT
{{client_context}}

OBJECTIVE
{{project_objective}}

CONSTRAINTS
{{scope_constraints}}

COMMERCIAL PREFERENCE
{{commercial_preference}}

TASK
Using the context, objective, and constraints above, produce a proposal structure covering, in this exact order:
1. Executive Summary — the challenge, the opportunity, and the proposed engagement in one framing statement
2. Current Trends — 2–4 industry/technology trends directly relevant to the client's domain (not generic trend lists)
3. Gap Analysis — current state vs. target state, organized by People/Process/Technology
4. Prioritized Scope — Must/Should/Could split, phased if the objective implies multiple stages
5. Approach & Delivery Model — how the work will run (methodology, cadence, quality gates)
6. Commercial Model — recommended pricing structure, respecting {{commercial_preference}} if provided, with 1–2 alternatives
7. High-Level Architecture — key layers/components implied by the objective and constraints (do not invent specific vendor products unless named in the context)
8. Capacity Plan — roles needed by phase and how team size should scale
9. Storyline — the talk-track sequence for presenting this proposal to the client (why now → what's broken → what good looks like → how we get there → investment → risks → next steps)
10. Assumptions & Exclusions — anything the model had to assume because it wasn't in the context, and anything explicitly out of scope

Output length: {{output_length}}

Follow the Output Format Instruction exactly: markdown H2 headers in the order above, bullets only, no preamble or closing remarks.
```

---

## Test Run (Author)

**Input values used:**
- `{{client_context}}` = "FedEx CloudOps — logistics/transportation, North America. Current: fragmented Azure and AWS estates managed by three regional teams with no shared runbook or cost governance."
- `{{project_objective}}` = "Consolidate CloudOps delivery under a single operating model within 6 months, reducing incident MTTR by 30% and cloud spend by 15%."
- `{{scope_constraints}}` = "Budget: $1.2–1.6M annually. Must retain SOC 2 Type II compliance. Azure-first, AWS secondary. No new vendor onboarding before Q2."
- `{{commercial_preference}}` = "Managed service with milestone-based transition pricing for the first 90 days."
- `{{output_length}}` = "Section headers + 2–3 bullet points per section, suitable for a 15-slide deck outline."

**Output quality:** Usable as-is for a first-draft deck outline — all 10 sections came back correctly ordered and scoped to the client context, though the Architecture section needed one manual edit to remove an assumed Kubernetes layer the brief never mentioned.

---

## Peer Review

**Reviewer:** Selva Kumar — Lead, Epam
**Date reviewed:** 2026-09-23
**Model used by reviewer:** Chat GPT

**Reviewer input values used:**
- `{{client_context}}` = "Regional retail bank, Canada. Current: legacy on-prem core banking with two failed cloud migration attempts in the last three years."
- `{{project_objective}}` = "Migrate core banking workloads to Azure within 12 months without disrupting branch operations."

| Review question | Reviewer answer |
|---|---|
| Could you run the template without asking the author anything? | Yes — the placeholder table and prompt body were self-explanatory; no clarification needed. |
| Was the output format what you expected? | Yes — clean H2 sections, bullets only, matched what I needed to paste straight into slide notes. |
| Would you use this template on your own work? | Yes — plan to reuse it for the next two client-lead proposal drafts this quarter. |
| One concrete improvement suggestion | Add an optional `{{industry_benchmark}}` placeholder so the Current Trends section can cite a specific stat instead of a generic trend statement. |

---

## Revision History

| Version | Date | Change | Author |
|---|---|---|---|
| 1.0 | 2026-09-22 | Initial commit | Punit Sharma |
| 1.1 | 2026-09-23 | Added Output Format Instruction constraint (bullets only, fixed section order) after peer review flagged inconsistent formatting on first pass; noted `{{industry_benchmark}}` as a candidate placeholder for v1.2 | Punit Sharma |
