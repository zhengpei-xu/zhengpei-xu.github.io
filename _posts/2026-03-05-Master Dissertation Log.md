---
title: 'Dissertation Research Log: Assessing cycling Network in the West Midlands using a LTN 1/20 adapted LTS Framework'
date: 2026-03-05
permalink: '/posts/2026/03/dissertation-log/'
tags:
  - Dissertation
  - Cycling
  - LTS
---

**Topic:** Adapting the Level of Traffic Stress (LTS) Framework to a UK Context  
**Case Study:** West Midlands Area  
**Supervisor:** Prof. Duncan Smith (UCL CASA)  
**Started:** March 2026

---
> See also: [Literature Reading](/literature-reading/)

## Log Entries


### 2026-03-05 — Supervisor Meeting #1

`Meeting` · Prof. Duncan Smith

- Spatial scale needs narrowing — confirm with TfWM that a scope adjustment is acceptable
- Road-level analysis cannot predict need for new infrastructure; frame limitations clearly
- Reference local council Low Traffic Neighbourhood (AKA.LTN) proposals and TfL Cycle Superhighways as context
- Quantifiable metrics for sub-criteria still unresolved
- ML methodology: role and application within the framework not yet defined

**Action Items**
- [ ] Follow up with TfWM on scope/scale adjustment
- [ ] Read Duncan and Philyoung's prior co-authored papers
- [ ] Identify available datasets for the West Midlands

**Open Questions**
- What is the appropriate spatial scale for this study?
- Which sub-criteria can realistically be quantified?

---

### 2026-03-12 — Methodology Development

`Writing` · LTS Framework Adaptation

Drafted the core rationale for the UK-adapted LTS framework. Existing frameworks were developed for the North American road environment; the proposed adaptation replaces American-origin thresholds with LTN 1/20 design standards — producing a framework directly grounded in the standards against which West Midlands cycling schemes will be assessed.

**Decisions Made**
- LTN 1/20 thresholds replace North American equivalents as the primary source of design standards
- Framework remains road-segment based (consistent with original LTS methodology)

**Still Unresolved**
- Intersection stress: how to map LTN 1/20 guidance onto intersection-level indicators
- Weighted aggregation vs. parallel dimensions — aggregation logic not yet decided

**Next Steps**
- [ ] Build indicator crosswalk table: LTS indicators ↔ LTN 1/20 equivalents
- [ ] Review Furth & Nixon (2016) intersection stress methodology

---

### 2026-04-22 — Data Ethics & TfWM Data Receipt

`Ethics` · `Admin`

UCL ethics forms in progress: Form A (Screening), Form B (Data Protection), Website Application.

Received data from TfWM this week:
- Compass IoT Near Miss Data
- iRAP Road Safety Assessment Star Ratings Data
- [TfWM Self-Serve portal](https://selfserve.datainsight.org.uk/mapview)

**Next Steps**
- [ ] Submit completed ethics forms
- [ ] Audit received datasets for completeness and coverage

---

### 2026-05-08 — Literature reading & Jeong's LTS Reproducibility

`Meeting` · `Coding`  

Reproducing Jeong's LTS Methodology:
- Getting a initial LTS map of West Midland Area
- Finishing reading Mekuri/ Conveyal/ Jeong's LTS (initially)  

While further reading / work are needed, especially concerning **the whole frame of methodology** (how to frame with LTN 1/20). Figuring out what TfWM can benefit from, and making the methods easier to understand. Maybe I have to build it under a wider background, should not be limited within LTS?

**Next Steps**
- [ ] Making some sliders for TfWM (DDL: 20/5/2026)
- [ ] presentation and communication with Jeong, preparing some questions in advance (DDL 13/5/2026)!!
- [ ] Buffer Zone: Do i really need it? do some reading.

---

### 2026-05-20 — TfWM Meeting: Deliverables Confirmed & Next Steps

`Meeting` · `Decision`

Met with TfWM. Callum confirmed the three final deliverables for the dissertation, so the overall direction is now locked in. The ask is clearly industry-facing — a commercial report plus a presentation suggests TfWM wants something they can actually use and circulate internally, not just an academic analysis. This also means the rationale for which LTN 1/20 metrics are included vs excluded needs to be very explicit: what can be answered with data, what can't, and why each one is in or out.

**Decisions Made**
- Final deliverables confirmed as three components:
  - a) A classification of LTN 1/20 metrics by operability — which can be quantified / improved through data, and which are inherently subjective and harder to fold into an automated network-scale assessment
  - b) A commercial report for TfWM
  - c) A final presentation to TfWM
- Next meeting (Fri 29/5) deliverables specified by Callum (see Next Steps)

**Open Questions**
- Format and depth of the commercial report — page count, structure, whether an executive summary is expected. Needs confirming with Callum.
- Criteria for including/excluding metrics — purely data availability, or also methodological rigour and TfWM's intended use case?
- Audience for the final presentation — technical team only, or also policy / decision-makers? This shapes the framing.

**Next Steps**
- [ ] Prepare slides for next Friday's meeting detailing progress so far (DDL: 29/5/2026)
- [ ] List which LTN 1/20 metrics will be answered, and which won't
- [ ] Write justification for excluded metrics (data limitation / subjectivity / scope)
- [ ] Finalise the LTN 1/20-enhanced LTS framework and send to Duncan for review
- [ ] Draft a plan for the next few weeks of data analysis work
- [ ] Compile potential interview questions (for stakeholders)

---

<!-- TEMPLATE

### YYYY-MM-DD — [Short title]

`Meeting` / `Writing` / `Data` / `Reading` / `Decision` / `Ethics` / `Admin`

[Narrative or bullet summary]

**Decisions Made**
**Open Questions**
**Next Steps**
- [ ] ...

-->