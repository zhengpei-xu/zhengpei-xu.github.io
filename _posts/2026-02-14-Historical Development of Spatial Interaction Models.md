---
title: 'Spatial Interaction Models: Historical Development and Formulations'
date: 2026-02-14
permalink: '/posts/2026/02/Spatial Interaction Models-Historical Development and Formulations/'
mathjax: true
tags:
  - Spatial Interaction Models
---

This summary traces the chronological development and refinement of Spatial Interaction Models (SIM) based on Michael Batty's lecture.

## Origins: The Gravity Model

The intellectual roots of spatial interaction models lie in an analogy with Newtonian physics. The first to apply gravitational logic to human movement was **Henry Carey (1858)**, who observed that human migration between cities followed patterns resembling gravitational attraction. This idea was formalised mathematically by **Ernst Ravenstein (1885)** in his *Laws of Migration*, where he established empirically that migration intensity decreases with distance.

The first explicitly gravitational formulation came from **E.G. Young (1924)** and was later popularised by **George Zipf (1946)**, who proposed the **P₁P₂/D rule**:

$$T_{ij} = k \frac{P_i P_j}{d_{ij}}$$

where $T_{ij}$ is the interaction between places $i$ and $j$, $P_i$ and $P_j$ are their populations, $d_{ij}$ is the distance separating them, and $k$ is a proportionality constant. This model treats population as the sole "mass" generating interaction, and assumes flows decay linearly with distance.

The astronomer **John Stewart (1941)** then introduced the concept of **demographic potential** — a measure of the cumulative gravitational pull exerted on one place by all others:

$$V_i = \sum_j \frac{P_j}{d_{ij}^\beta}$$

Stewart's contribution was to generalise the distance exponent to $\beta$, recognising that the rate of distance decay was an empirical question rather than a physical constant. This $\beta$ parameter — the **distance decay parameter** — became the central object of interest in all subsequent SIM development. A high $\beta$ means flows are very sensitive to distance (steep decay); a low $\beta$ means people are willing to travel further.



## The General Gravity Model

Building on Stewart and Zipf, the **general unconstrained gravity model** takes the form:

$$T_{ij} = k \cdot V_i^\mu \cdot W_j^\alpha \cdot d_{ij}^{-\beta}$$

| Term | Definition | Role |
|---|---|---|
| $T_{ij}$ | Predicted flow from $i$ to $j$ | Dependent variable |
| $k$ | Global scaling constant | Calibrates total flow volume |
| $V_i$ | Origin mass (e.g. population) | Measures emissiveness of origin |
| $W_j$ | Destination mass (e.g. store area, jobs) | Measures attractiveness of destination |
| $d_{ij}$ | Distance or cost between $i$ and $j$ | Deterrence term |
| $\mu, \alpha$ | Mass sensitivity parameters | How strongly origin/destination size drives flows |
| $\beta$ | Distance decay parameter | How rapidly flows diminish with distance |

The parameters $\mu$, $\alpha$, and $\beta$ are estimated from observed flow data. **No marginal totals are constrained** — both origin and destination flows are free to vary. This makes the model maximally flexible but less predictively accurate, since it cannot guarantee that predicted flows sum to known totals.

**Typical applications:** inter-regional trade flows; early migration studies; telephone communication patterns — any context where neither origin totals nor destination totals are independently known.



## Wilson's Entropy-Maximising Framework and the SIM Family (1967–71)

The most important theoretical advance came from **Alan Wilson (1967, 1971)**, who derived the entire family of spatial interaction models from first principles using **entropy maximisation**. Rather than relying on the physics analogy, Wilson asked: *given what we know about total flows, what is the most probable distribution of individual trips?* Maximising entropy subject to constraints on observed totals yields exactly the gravity model family — but now with a rigorous statistical foundation.

Crucially, Wilson showed that the appropriate model form depends entirely on **which marginal totals are known and should be treated as constraints**. This gave rise to three distinct models.



### Unconstrained Model

Used when neither $O_i$ nor $D_j$ are known. Wilson showed this corresponds to maximising entropy with only a constraint on total travel cost.

$$T_{ij} = k \cdot V_i^\mu \cdot W_j^\alpha \cdot f(c_{ij})$$

**Typical applications:** exploratory analysis of interaction patterns; inter-regional trade; contexts where no marginal totals can be independently observed.



### Production-Constrained Model

When the total flow **leaving each origin** $O_i$ is known (e.g. total shopping trips from a residential zone, derived from population), it should be held fixed. Wilson introduced a **balancing factor** $A_i$ to enforce this:

$$T_{ij} = A_i \cdot O_i \cdot W_j^\alpha \cdot f(c_{ij})$$

$$A_i = \frac{1}{\displaystyle\sum_j W_j^\alpha \cdot f(c_{ij})}$$

The constraint satisfied is:

$$\sum_j T_{ij} = O_i \quad \forall i$$

| Term | Definition |
|---|---|
| $O_i$ | Known total outflow from origin $i$ (fixed) |
| $A_i$ | Balancing factor ensuring outflows are conserved |
| $W_j^\alpha$ | Destination attractiveness with sensitivity $\alpha$ |
| $f(c_{ij})$ | Cost/deterrence function (e.g. $e^{-\beta c_{ij}}$) |
| $\beta$ | Distance decay parameter (estimated from data) |

Here $\alpha$ and $\beta$ are the only free parameters — origin mass is already encoded in $O_i$. The destination inflows $\sum_i T_{ij}$ are a **model output**, not an input.

**Typical applications:** retail catchment modelling (flows from residential zones to supermarkets); journey-to-work where census commuter totals by origin are available; school choice modelling.



### Attraction-Constrained Model

Symmetrically, when total **inflow to each destination** $D_j$ is known but origin totals are not:

$$T_{ij} = B_j \cdot V_i^\mu \cdot D_j \cdot f(c_{ij})$$

$$B_j = \frac{1}{\displaystyle\sum_i V_i^\mu \cdot f(c_{ij})}$$

The constraint satisfied is:

$$\sum_i T_{ij} = D_j \quad \forall j$$

**Typical applications:** modelling flows *to* a fixed-capacity facility (hospital, airport) where total admissions or passengers are known; migration to cities where in-migration totals are recorded.



### Doubly Constrained Model

When **both** $O_i$ and $D_j$ are known, both sets of balancing factors are applied simultaneously:

$$T_{ij} = A_i \cdot O_i \cdot B_j \cdot D_j \cdot f(c_{ij})$$

$$A_i = \frac{1}{\displaystyle\sum_j B_j D_j f(c_{ij})}, \qquad B_j = \frac{1}{\displaystyle\sum_i A_i O_i f(c_{ij})}$$

Since $A_i$ depends on $B_j$ and vice versa, these are solved **iteratively** (the Furness/IPF procedure) until convergence. Both constraints are satisfied simultaneously:

$$\sum_j T_{ij} = O_i \quad \forall i \qquad \text{and} \qquad \sum_i T_{ij} = D_j \quad \forall j$$

The only free parameter is $\beta$ — both mass terms are fully determined by observed data, leaving only the distance decay to estimate.

**Typical applications:** transport planning trip distribution (four-step model); inter-regional migration where both in- and out-migration totals come from the census; freight movement between fixed origin and destination terminals.



## The Role of the Cost Function

All three constrained models require specifying $f(c_{ij})$. Two standard forms are:

| Form | Equation | Properties |
|---|---|---|
| Power | $c_{ij}^{-\beta}$ | Heavy-tailed; suitable for long-distance flows |
| Negative exponential | $e^{-\beta c_{ij}}$ | Steep short-distance decay; preferred for urban trips |

For supermarket shopping — short, frequent, and urban — the **negative exponential** is standard, as most people are unwilling to travel more than a few kilometres and the deterrence effect is sharp.



## Summary

| Model | Constraints | Free Parameters | Primary Use |
|---|---|---|---|
| Unconstrained | None | $k, \mu, \alpha, \beta$ | Exploratory, no known totals |
| Production-constrained | $O_i$ fixed | $\alpha, \beta$ | Retail, commuting (known origins) |
| Attraction-constrained | $D_j$ fixed | $\mu, \beta$ | Facility planning (known capacities) |
| Doubly constrained | $O_i$ and $D_j$ fixed | $\beta$ only | Transport planning, migration |

Wilson's framework showed that these are not four separate models but **one unified family**, differentiated only by which empirical constraints are imposed. This theoretical unification, combined with the entropy-maximising derivation, transformed spatial interaction modelling from a physics analogy into a rigorous applied framework — and laid the foundation for every land use and transport model that followed.



## References

Carey, H.C. (1858) *Principles of Social Science*. Philadelphia: J.B. Lippincott.

Fotheringham, A.S. and O'Kelly, M.E. (1989) *Spatial Interaction Models: Formulations and Applications*. Dordrecht: Kluwer Academic Publishers.

Furness, K.P. (1965) 'Time function iteration', *Traffic Engineering and Control*, 7(7), pp. 458–460.

Hansen, W.G. (1959) 'How accessibility shapes land use', *Journal of the American Institute of Planners*, 25(2), pp. 73–76.

Ravenstein, E.G. (1885) 'The laws of migration', *Journal of the Statistical Society of London*, 48(2), pp. 167–235.

Stewart, J.Q. (1941) 'An inverse distance variation for certain social influences', *Science*, 93(2404), pp. 89–90.

Wilson, A.G. (1967) 'A statistical theory of spatial distribution models', *Transportation Research*, 1(3), pp. 253–269.

Wilson, A.G. (1971) *Entropy in Urban and Regional Modelling*. London: Pion.

Zipf, G.K. (1946) 'The P1 P2/D hypothesis: On the intercity movement of persons', *American Sociological Review*, 11(6), pp. 677–686.
