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
