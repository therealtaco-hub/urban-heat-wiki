---
title: "Source: Cavan et al. 2014 — GRaBS Assessment Tool & STAR Tools"
type: source
tags: [interactive-tools, gis-dss, vulnerability, separate-modules, pre-calculated, manchester, europe, closest-prior-tool]
sources: 1
updated: 2026-08-18
---

# Source: Web-GIS Tools for Climate Change Adaptation Planning in Cities

- **Type:** book chapter
- **Author(s):** Gina Cavan, Tom Butlin, Susannah Gill, Richard Kingston, Sarah Lindley
- **Date:** 2014
- **Venue:** *Handbook of Climate Change Adaptation*, Springer, DOI 10.1007/978-3-642-40455-9_106-1
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/Web-GIS tools for climate change adaptation planning in cities.PDF` in the code project
- ⭐⭐ **Closest prior tool** — see redundancy/lineage note in [[wiki/sources/smith-2009-manchester-gis-dss]] (same Manchester research group, earlier forerunner).

## Summary
This chapter documents the two web-GIS tools built for the EU GRaBS project (Green and Blue Space Adaptation for Urban Areas and Eco Towns, 2008–2011, 14 European partners across 10 municipalities): the **GRaBS Climate Change Risk and Vulnerability Assessment Tool** and the **Surface Temperature and Runoff (STAR) Tools**. It opens with a structured review of the state-of-the-art in online climate-adaptation decision tools circa 2009–2014, categorizing them into five types (process-oriented frameworks, portals, generic assessment techniques, high-level screening models, and detailed offline models) and finding "no existing tool specifically for vulnerability assessment" and a general "scarcity of tools specifically focused on cities."

The **Assessment Tool** is a Google-Maps-based Public Participation GIS with 350+ pre-processed spatial data layers (green/blue space, vulnerability indicators like people aged 75+ and low-income residents, social/civil infrastructure, hazard zones, population structure) that users can overlay to visually assess spatial coincidence of risk factors — explicitly categorized by the authors themselves as a "high-level or screening tool" because "the data used in the model is processed offline and the tool does not involve real-time processing of models." The **STAR Tools** were added later specifically to enable "what-if" scenario modeling that the static Assessment Tool couldn't provide: a **Surface Temperature Tool** (urban climate model predicting max surface temperature on the 98th-percentile hottest summer day, as a function of land-cover mix) and a **separate Surface Runoff Tool** (US Soil Conservation Service method, predicting runoff volume/percentage as a function of land cover and soil type) — two independent tools, each run separately, with results only combinable manually afterward in external GIS if a user runs both across multiple neighborhoods.

## Key Claims
1. As of this chapter's 2014 review of the state of the art, **no tool existed that combined heat/temperature modeling and surface-water/runoff modeling in a single integrated interface** — the STAR Tools are explicitly two separate tools (ST Tool, SR Tool), each independently run, each with its own underlying model — this is the single strongest, most concrete piece of evidence in the entire source set for this project's "separate modules" gap claim, coming directly from the authors of the closest comparable prior tool.
2. The GRaBS Assessment Tool integrates vulnerability (including an elderly/low-income indicator layer) with hazard data, but only as **overlaid, browsable static layers** — not a computed composite index, and not combined with any live simulation capability; "what if" scenario modeling was explicitly identified by GRaBS partners themselves as a *missing* capability that motivated building the separate STAR Tools afterward.
3. STAR Tools' "what if" mechanic (add or remove a fixed % of green cover, reallocated proportionally from/to other surface types — impervious first, then roads, buildings, bare soil) is conceptually close to this project's unsealing slider, but crucially the STAR Tools are **not interactive/live in a browser session** the way this project's sliders are — the demonstrated Mersey Forest Plan application ran the Surface Temperature Tool for 210 wards as a batch process, then mapped results afterward in separate GIS software; there is no described real-time, single-session what-if interaction loop for an individual user exploring their own area interactively.
4. Explicit SWOT analysis of the broader adaptation-tool landscape (as of ~2009–2014) found tools generally "handle physical aspects very well but are not as good on socioeconomic factors" and have a "lack of consideration of cross-sectoral interactions" — precisely the two-separate-dimensions problem (physical/heat vs. socioeconomic/vulnerability) this project's integrated tool addresses.
5. Even the mature, EU-funded, 10-city-deployed GRaBS tools were fundamentally screening/pre-calculated tools rather than live simulators — reinforcing that the "live, user-adjustable, single-session what-if simulation" capability this project offers was still a genuine gap even in the most developed prior European tool of its kind.
6. Practical deployment data: STAR Tools had only ~1,100 unique visitors and ~200 completed sessions in its first two years (as of Dec 2013) — useful context on how niche/underused even a well-funded EU climate-adaptation tool project remained, arguably supporting an accessibility-focused design case.

## Data and Figures
- GRaBS project: 2008–2011, 14 partners, 10 municipalities across the EU; Assessment Tool: 350+ data layers (32 EU-wide + 7–60+ per-partner local layers).
- STAR Tools usage (as of Dec 2013): ~1,100 unique visitors, ~200 progressed to a results page; 64% UK-origin traffic.
- Mersey Forest Plan case study: Surface Temperature Tool run across 210 wards; hottest ward (Liverpool Central) 31.7°C max surface temp vs. coolest (Tilston, Cheshire) 18.3°C — a 13.4°C spread, strongly correlated with green-cover percentage (16.7% vs. 97.7% green respectively).
- STAR Tools applicable scale: 0.4 ha – 4 km² ("neighbourhood" scale).

## Contradictions / Gaps
- This is the strongest and most citable "separate modules" precedent in the whole source set — use it as the anchor citation for the paper's gap statement, not just one example among several.
- Pre-calculated/screening architecture (not live simulation) — the same limitation as Smith et al. 2009, its own forerunner; cite Smith 2009 only briefly as lineage, give this chapter the full treatment.
- No description anywhere of a live, single-session interactive slider/parameter-adjustment loop — the closest the STAR Tools get is entering custom land-cover/climate parameters for one's own study area before a batch run, not real-time feedback as parameters change.
- No indication the Assessment Tool's vulnerability layers were ever combined into a single computed vulnerability score (unlike this project's HVI) — vulnerability remains a set of separately-browsable map layers throughout.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/interactive-climate-tools]] (new)
- [[wiki/concepts/entsiegelung]]
- [[wiki/entities/manchester]] (new)
- [[wiki/index]]
