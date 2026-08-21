---
title: "Source: Smith et al. 2009 — GIS-Based DSS for Urban Climate Risk, Manchester"
type: source
tags: [interactive-tools, gis-dss, vulnerability, pre-calculated, foundational, manchester, uk]
sources: 1
updated: 2026-08-18
---

# Source: A GIS-Based Decision Support Tool for Urban Climate Risk Analysis and Exploration of Adaptation Options, with Respect to Urban Thermal Environments

- **Type:** paper (conference)
- **Author(s):** Claire L. Smith, Sarah J. Lindley, Geoff J. Levermore, Susan E. Lee (University of Manchester)
- **Date:** 2009
- **Venue:** ICUC7 — 7th International Conference on Urban Climate, 29 June – 3 July 2009, Yokohama, Japan (4-page conference paper, no DOI)
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/A_GIS-based_decision_support_tool_for_urban_climat.pdf` in the code project
- ⚠️ **Lineage note:** this is an early forerunner of the same University of Manchester research group's later GRaBS Assessment Tool (see [[wiki/sources/cavan-2014-grabs-star-tools]], Sarah Lindley co-authors both). When drafting, cite this only briefly as the historical origin point — do not treat it as an independent data point alongside Cavan et al. 2014, which documents the mature, multi-city-deployed version of the same tool lineage.

## Summary
A short (4-page) early-stage description of a GIS-based decision-support tool developed for Greater Manchester, UK, in response to a 2007 UK policy requirement (National Indicator 188) that local authorities demonstrate an adaptive response to climate risk. The tool combines: (1) hazard data — current/future spatial temperature patterns built by downscaling the HadRM3 regional climate model (25km → 5km via stochastic weather generator → ~200m via an empirical model using distance-from-urban-centre, surface cover, and building density as predictors, calibrated against airborne/ground thermal transects); (2) vulnerability data — split into socio-economic vulnerability (census-based age/health/wellbeing) and building vulnerability (density, height, age, use, orientation, proximity to greenspace); and (3) a catalog of pre-defined adaptation options (green roofs, shading, glazing changes, natural ventilation, orientation) that a user can explore, each pre-scored for its temperature/emissions/heat-emission impact.

Critically, the tool explicitly states it "does not allow on-the-fly processing" — all adaptation-option outcomes shown to the user are pre-calculated using an offline mesoscale climate model, emission inventories, and DesignBuilder building simulations, then looked up rather than computed live in response to user input.

## Key Claims
1. As early as 2009, a UK research group was already combining heat hazard + socio-economic vulnerability + building vulnerability + adaptation-option exploration in one GIS-based decision-support tool at city/neighbourhood/building scale — direct historical precedent for exactly this project's three-part (heat + vulnerability + intervention-simulation) integration ambition, 15+ years before this project.
2. The tool is explicitly a *lookup* tool, not a live simulator: "the tool does not allow on the fly processing," with all adaptation-option impacts pre-calculated offline and presented as static reports/maps — a clean, citable contrast against this project's live-slider architecture (`/api/simulate/baeume`, `/api/simulate/wasser` compute on request from user-supplied parameters, not from a pre-computed lookup table).
3. Vulnerability is explicitly split into two separate tracks (socio-economic vs. building vulnerability) that are not combined into a single unified score in the paper as described — risk emerges from spatial overlay of separately-visualized layers, not a single computed index.
4. The empirical downscaling model (city → neighbourhood, ~200m) uses building density and surface cover as predictors, calibrated against real airborne/ground thermal-transect measurements — methodologically analogous to (though predating) this project's LST↔Zensus 100m-grid approach, but using downscaled climate-model output rather than direct satellite LST retrieval.
5. Adaptation options are pre-defined and pre-scored per building/development type (new vs. existing), not user-parameterized (e.g. there is no equivalent of "how many trees" or "how many m² unsealed" — options are binary yes/no choices from a fixed catalog).

## Data and Figures
- Hazard downscaling chain: HadRM3 (25km) → stochastic weather generator (5km) → empirical surface-cover/density model (~200m, scalable).
- Adaptation option catalog: city-scale (workplace/remote-work scenarios), neighbourhood-scale (orientation, layout, green/blue space integration), building-scale (envelope, green roofs, glazing, shading, ventilation, HVAC), each tagged for applicability to new vs. existing development.
- No quantitative cooling coefficients or effect-size figures are reported in this short conference paper (unlike the fuller STAR Tools description in Cavan et al. 2014).

## Contradictions / Gaps
- Pre-calculated/lookup-based adaptation impacts vs. this project's live, user-parameterized simulation — a clean, quotable early contrast, but keep the citation brief given its lineage overlap with Cavan et al. 2014 (see redundancy note above).
- No unified vulnerability score — vulnerability is presented as separate overlay layers, not combined into a single index the way this project's HVI does.
- Very short paper (4 pages, conference proceedings, no DOI) — thin on methodological detail and has no validation/evaluation section; cite for historical framing only, not for any quantitative claim.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/interactive-climate-tools]] (new)
- [[wiki/entities/manchester]] (new)
- [[wiki/index]]
