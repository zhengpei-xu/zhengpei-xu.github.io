---
title: 'Literature Reading'
date: 2026-03-19
permalink: '/literature-reading/'
tags:
  - Dissertation
  - LTS
  - Cycling
---

**Dissertation:** Assessing cycling Network in the West Midlands using a LTN 1/20 adapted LTS Framework  



## Index

| # | Author(s) | Year | Title | Theme | Priority | Status |
|---|-----------|------|-------|-------|----------|--------|
| 00 | sample | sample | sample | sample | sample | `unread` |
| 01 | Jeong, P. and Smith, D | 2025 | Improving Infrastructure and Accessibility Indicators for Urban Cycling Networks | `lts-framework` | `core` | `done` |
| 02 | Mekuria et al. | 2012 | Low-Stress Bicycling and Network Connectivity | `lts-framework` | `core` | `reading` |

> **Theme tags:** `lts-framework` `ltn-1/20` `cycling-stress` `network-analysis` `uk-policy` `west-midlands` `intersection` `methodology`
>
> **Priority:** `core` `related` `background`
>
> **Status:** `unread` `reading` `done` `needs-revisit`


### [01] Jeong & Smith (2025) — Improving Infrastructure and Accessibility Indicators for Urban Cycling Networks

> **Zotero key:** `jeong2025`  
> **Themes:** `lts-framework`  
> **Priority:** `core` | **Status:** `done`

**Core argument**

Uses cycling infrastructure data and accessibility metrics to build a measurement framework for tracking cycling network improvement, applied to London using OSM-derived data and an enhanced LTS model.

**Relevance to dissertation**

Data sources used:
- `pyrosm` — road classification, cycle infrastructure type, lane count, speed limits, POIs
- Census data (LSOA level) — population, journey to work
- TfL link-level count data
- Survey data — 2011 & 2021 journey to work; Active Lives Survey (DfT 2024)

Methodology:
1. Derive cycling networks from OSM (pre-processing, adding unprotected advisory lanes, mapping OSM tags to road types)
2. Enhance Conveyal LTS model — English road type scoring, new intersection measurement (traffic lights, stop signs)
3. Add preference weights based on TfL route choice (off-road / protected lane / etc.)
4. Normalise scores into LTS level segmentation
5. Use edge betweenness centrality to calculate demand flow

**Limitations / Questions**
---



### [02] Mekuria et al. (2012) — Low-Stress Bicycling and Network Connectivity

> **Zotero key:** `mekuria2012`  
> **Themes:** `lts-framework`  
> **Priority:** `core` | **Status:** `reading`

**Core argument**

**Relevance to dissertation**

**Limitations / Questions**
---

### [03] Furth et al. (2018) — Measuring Low-Stress Connectivity in Terms of Bike-Accessible Jobs and Potential Bike-to-Work Trips (Delaware case study, JTLU)

> **Zotero key:** `furth2018`  
> **Themes:** `LTS v2.0`, `ADT integration`, `job accessibility`, `network connectivity`  
> **Priority:** `Essential` | **Status:** `Read`

**Core argument**

Introduces LTS Revision 2.0, updating the original Mekuria criteria based on practitioner feedback from Delaware DOT and Arlington County, VA. The biggest change is adding Average Daily Traffic (ADT) as an input for mixed-traffic segments, motivated by the "triple encounter" concept — when a cyclist, an oncoming vehicle, and a following vehicle meet simultaneously, forcing the following vehicle to either slow down or pass with scant clearance. Key threshold: 1+1 lane roads at 25–30 mph become LTS 3 at ADT > 1,500 (based on Arlington citizen complaints about N. Lexington Street). Also expands speed range (adds 20 mph low end, refines high-speed categories for rural roads), provides explicit one-way street rules, makes bike lane width a factor at higher speeds, simplifies bike lane blockage treatment (treat as mixed traffic), and adds unsignalised intersection right-turn lane criteria. Demonstrates the updated framework through a Delaware case study linking LTS-based low-stress connectivity to bike-accessible jobs and potential bike-to-work trips.

**Relevance to dissertation**

- Primary reference for understanding version evolution from Original to v2.0; Section 2 provides the cleanest summary of every change and its rationale — essential for lit review.
- ADT integration is directly relevant: TfWM's Vivacity traffic count data can supply this variable, making v2.0 more applicable to West Midlands than the Original.
- Rural road criteria expansion matters for West Midlands' mixed urban-rural geography.
- The job accessibility / connectivity analysis framework is a methodological precedent for network-scale evaluation.
- Weakest-link aggregation from segment to route level informs how CLoS segment scores should aggregate in my framework.
- Intersection treatment remains limited (right-turn lane criteria developed but not applied due to data absence) — confirms the gap my JAT integration could fill.

**Limitations / Questions**

- All ADT thresholds (e.g., 1,500 for 1+1 lane roads) are calibrated to US driving behaviour and road geometry. Need to critically assess whether these transfer to UK context or whether LTN 1/20 provides UK-appropriate equivalents.
- Speed limits in mph throughout; UK uses mph but road design conventions differ (e.g., 20 mph zones are now widespread in UK urban areas — how does this interact with v2.0's new 20 mph category?).
- One-way street rules assume US conventions; UK one-way systems and contraflow cycling provisions may need different treatment.

---

### [04] Providelo et al. (2021) — Assessing the Applicability of LTS to a Medium-Sized City in a Developing Country (Brazil)

> **Zotero key:** `providelo2021`  
> **Themes:** `LTS validation`, `physiological stress measurement`, `context transferability`, `Global South`  
> **Priority:** `High` | **Status:** `Read`

**Core argument**

Tests whether LTS classifications match actual physiological stress levels (measured from cyclists during real rides) in a Brazilian medium-sized city. Finds discrepancies between LTS classifications and measured stress, suggesting that LTS criteria developed for North American/Dutch contexts do not directly transfer to different urban environments. Identifies stressors not captured by the original LTS framework.

Adding features of *gradient* and *Roundabout* to improve the framework

**Relevance to dissertation**

- Strongest empirical evidence that LTS requires context-specific adaptation — directly supports the rationale for my UK adaptation.
- The finding that original criteria miss locally relevant stressors parallels my argument that UK-specific factors captured by LTN 1/20 (e.g., junction treatment, cycling infrastructure design details) are absent from Mekuria/Furth criteria.
- Methodological note: they used physiological measurement as ground truth. My dissertation does not have this, but TfWM's Compass IOT near-miss data could serve as a partial behavioural proxy for stress validation.

**Limitations / Questions**

- Brazilian medium-sized city is a very different context from UK metropolitan region — useful for the "LTS needs adaptation" argument but not directly comparable.
- Physiological stress ≠ perceived stress ≠ infrastructure quality. My approach measures infrastructure quality (via CLoS/JAT), not stress directly. Need to be clear about this distinction.

---

### [05] Harvey, Rodríguez & Fang (2024) — Comparing Methods and Data Sources for Classifying Bicycle Level of Traffic Stress: How Well Do Their Outcomes Agree?

> **Zotero key:** `harvey2024`  
> **Themes:** `LTS commensurability`, `method comparison`, `data source effects`, `OSM`, `complexity-consistency tradeoff`  
> **Priority:** `Essential` | **Status:** `Read`

**Core argument**

Systematically compares 7 LTS methods × 3 data sources (audit, OSM, local agency GIS) across Portland and Austin. Finds substantial disagreement between methods: weighted kappa ranges from 0.18 (slight) to 0.99 (almost perfect). Two counter-intuitive findings: (1) the least precise data source (OSM) produced the most consistent results across methods (median κ = 0.89 vs 0.50 for audit data), because its "fuzziness" from missing-data assumptions reduced opportunity for divergent interpretations; (2) the simplest method (Conveyal, 4 variables, 7 rules) had the highest cross-data-source consistency (median κ = 0.91). Extreme example: one Portland block (NW Glisan St 500) received all four LTS levels depending on method-data combination. Recommends using simpler methods for commensurable network-scale screening and detailed site studies for segment-level precision. Strongly advocates clear labelling of LTS method and data source.

**Relevance to dissertation**

- **Key argument 1: Narrowing the gap.** Harvey demonstrates that methodological fragmentation drives classification inconsistency. My adaptation anchors LTS criteria to LTN 1/20, a nationally endorsed design standard with institutional legitimacy (used by Active Travel England for scheme funding appraisal). This replaces arbitrary, researcher-defined thresholds with standardised engineering criteria, directly addressing the commensurability problem Harvey identifies.
- **Key argument 2: Bridging the scale dichotomy.** Harvey frames network-scale LTS and site-level assessment as a necessary tradeoff. My approach dissolves this dichotomy: LTN 1/20's CLoS and JAT are inherently site-audit standards, but by operationalising them within a network-scale LTS framework — leveraging TfWM's high-granularity sensor data (Vivacity counts, Compass IOT near-miss, speed surveys) — network-wide assessment can achieve site-study rigour. This has direct practical value for transport authorities and local councils prioritising cycling infrastructure investment.
- **Policy implication:** Since Active Travel England uses CLoS/JAT to evaluate funding applications, a network-scale tool that automatically identifies low-scoring segments provides actionable pre-screening for where to apply for improvement funding.
- Table 1 (variable comparison across methods) is an excellent template for presenting my own method's variable requirements alongside existing LTS variants.

**Limitations / Questions**

- Harvey does not evaluate which method is most *accurate* (no independent stress measure as ground truth), only *consistency*. My LTN 1/20-based approach claims greater validity through institutional backing, but this is a design-standard argument, not an empirical-validation argument.
- The finding that more precise data increases disagreement could be turned against my approach: TfWM's granular data might expose more edge cases where CLoS/JAT scoring is ambiguous. Need to anticipate this in methodology.
- Harvey's recommendation for simpler methods tensions with my approach adding LTN 1/20 complexity. Counter-argument: the complexity is in the *standard* (which is externally defined and validated), not in ad hoc researcher decisions.

---



### [00] Author(s) (Year) — Title

> **Zotero key:** `authorYYYY`  
> **Themes:** `...`  
> **Priority:** `...` | **Status:** `...`

**Core argument**

**Relevance to dissertation**

**Limitations / Questions**
---

<!--
INSTRUCTIONS FOR ADDING A NEW ENTRY
1. Add a row to the Index table above
2. Copy the block below, paste at the bottom of the Notes section
3. Fill in all fields; delete comment lines when done

---

### [NN] Author(s) (Year) — Title

> **Zotero key:** `authorYYYY`
> **Themes:** `...`
> **Priority:** `...` | **Status:** `...`

**Core argument**

**Relevance to dissertation**

**Limitations / Questions**

-->
