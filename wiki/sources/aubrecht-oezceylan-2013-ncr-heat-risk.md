---
title: "Source: Aubrecht & Özceylan 2013 — Heat Risk Patterns, U.S. National Capital Region"
type: source
tags: [vulnerability, hvi, lst, census-block, equal-weight, crichton-risk-triangle, usa]
sources: 1
updated: 2026-08-18
---

# Source: Identification of heat risk patterns in the U.S. National Capital Region by integrating heat stress and related vulnerability

- **Type:** paper
- **Author(s):** Christoph Aubrecht, Dilek Özceylan
- **Date:** 2013 (received 2012-11-25, accepted 2013-03-13, online 2013-04-17)
- **Venue:** *Environment International* 56:65–77, DOI 10.1016/j.envint.2013.03.005
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/1-s2.0-S0160412013000676-main.pdf` in the code project

## Summary
This is the closest methodological precedent in the project's literature base to its own HVI construction. Aubrecht & Özceylan build a **Heat Stress Risk Index (HSRI)** for the Washington D.C. metro area ("National Capital Region", ~5.5M population, 22 counties, ~53,500 populated census blocks) at the finest available spatial unit (U.S. census block). The index is the product of a **Heat Stress Index (HSI)** — a kriging-interpolated grid of annual heat-wave-day counts (2010) from ~140 weather stations, normalized 0–1 — and a **Heat Stress Vulnerability Index (HSVI)** — six equally-weighted, min-max normalized socioeconomic/demographic indicators (age 65+, living alone, poverty, poor English skills, low education, and green-cover as a protective/negative factor), all from U.S. Census 2010 and American Community Survey (ACS) 5-year estimates. Critically, the paper explicitly chooses **equal-weighted, un-transformed additive aggregation over PCA/factor analysis**, arguing this avoids introducing additional subjectivity into the index — the same philosophical stance as this project's fixed literature-derived 0.6/0.4 weighted-sum HVI.

The results show that risk patterns are driven primarily by the vulnerability distribution rather than by hazard alone: the District of Columbia core is characterized by very high risk index values (64% of populated D.C. census blocks classified high/very-high risk) despite not experiencing the year's peak heat-wave-day counts — because vulnerability (age, poverty, isolation) is spatially concentrated there. The paper concludes with an explicit call for fine-scale, sub-county heat vulnerability mapping to enable targeted resource allocation and municipal heat-response planning.

## Key Claims
1. Equal-weighted, additive aggregation of normalized 0–1 vulnerability indicators is explicitly preferred over PCA/factor analysis "to avoid additional subjectivity" — since no single variable's dominance is supported by the literature in a heat-specific context. This is the strongest direct precedent for this project's own fixed-weight (not PCA-derived) HVI design philosophy.
2. Risk = Hazard × Vulnerability (multiplicative, Crichton's Risk Triangle), computed at the finest available census unit (census block), then class-binned via Jenks natural-breaks into 5 categories (very low–very high) to reduce over-interpretation of individual raw values.
3. About 80% of older adults (65+) have at least one chronic condition that increases heat vulnerability, and elderly people living alone face compounded risk from reduced ability to get help during an emergency — direct epidemiological grounding for weighting elderly share as a vulnerability proxy (cites CDC/epidemiological literature).
4. Fine spatial resolution reveals patterns invisible at coarser (county) scale: only 4% of the whole NCR study area is highly/very-highly vulnerable, but 64% of Washington D.C.'s populated blocks are — a stark illustration of why sub-city-scale HVI mapping (as opposed to city- or county-average scores) is necessary for targeting adaptation resources.
5. Health-outcome data (mortality, morbidity, insurance coverage) could not be integrated into the fine-scale index because such data in the U.S. is only available at county level or coarser — the same "no fine-grained health data" constraint this project faces with Zensus data (no health variables at 100m grid).
6. The paper explicitly flags composite-index construction as inherently uncertain (indicator selection, weighting, and coupling effects can all amplify results) but argues indices remain valuable for "encapsulating a complex reality in a single measurable construct" that supports decision-making despite that uncertainty.

## Data and Figures
- Study area: Washington D.C. metro area (NCR), ~5.5M population, 22 counties, ~92,000 census blocks (~53,500 populated).
- HSI: annual 2010 heat-wave-day count (≥3 consecutive days with Tmax≥30°C), kriged from ~140 stations at 0.5km output resolution.
- HSVI: 6 equal-weighted indicators — age 65+, living-alone elderly, poverty ratio, poor-English ratio, low-education ratio, green-area ratio (inverse/protective).
- 87% of NCR land area = low/very-low vulnerability, covering only 44% of populated census blocks (smaller, denser urban blocks skew high-vulnerability).
- D.C. core: 64% of populated blocks classified high/very-high risk vs. only 4% for the full NCR region.

## Contradictions / Gaps
- Multiplicative hazard×vulnerability combination, not additive weighted-sum like this project's HVI — worth an explicit methodological note in Methods (this project sums a normalized LST term and a normalized elderly-share term rather than multiplying a hazard index by a vulnerability index).
- No Bayesian/empirical-Bayes shrinkage for small-population census blocks — same gap noted in the other Cluster 2 sources; this project's `shrink_senior_rate()` / N_PRIOR=50 correction addresses exactly the kind of small-numbers instability Aubrecht & Özceylan's block-level analysis would also be exposed to (their paper does not discuss it).
- U.S. Census/ACS-specific indicators (poor English skills, health-insurance access) have no direct Zensus 2022 equivalent — this project's HVI necessarily uses a narrower indicator set (age only, no income/language/health proxy) due to German data-protection-driven data availability at 100m grid.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/heat-vulnerability-index]] (new)
- [[wiki/index]]
