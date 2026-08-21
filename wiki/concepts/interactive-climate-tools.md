---
title: "Interactive Climate Adaptation Tools / Decision-Support Systems"
type: concept
tags: [interactive-tools, digital-twin, gis-dss, decision-support, novelty-anchor]
sources: 5
updated: 2026-08-18
---

# Interactive Climate Adaptation Tools / Decision-Support Systems

This concept covers software tools that let a non-expert user (urban planner, policymaker, citizen) explore climate-adaptation "what-if" scenarios for a city — as opposed to tools that only *describe* current conditions via static maps. This is the category that defines this project's own novelty claim: no source reviewed integrates heat, social vulnerability, and surface-water/unsealing in one live, coefficient-based, interactively-adjustable tool.

## Key Facts
- As of a 2014 state-of-the-art review, **no tool existed combining heat/temperature and surface-water/runoff modeling in one integrated interface** — the closest prior tool (STAR Tools, [[wiki/sources/cavan-2014-grabs-star-tools]]) ships them as two *separate*, independently-run tools.
- Every digital-twin/physics-based tool reviewed for this project (Lahti, Singapore DUCT, UMEP-TARGET) is LST/temperature-only — **none integrate a social-vulnerability dimension**.
- There is a consistent trade-off axis across all reviewed tools between physical accuracy/sophistication and accessibility: heavyweight physics models (WRF+PALM-4U in DUCT) require HPC-scale compute (thousands of core-hours) and proprietary agency data; lightweight physics models (TARGET/UMEP) run in under an hour on a desktop but still require GIS software and expert data preparation (DSM/DEM, land-cover rasters); ML-based tools (Lahti digital twin) are fast and accessible but are black-box and score lowest on user trust in their own evaluation.
- Even the most mature, EU-funded, 10-city-deployed prior tool (GRaBS Assessment Tool + STAR Tools) is fundamentally a **screening/pre-calculated** system — "the tool does not involve real-time processing of models" ([[wiki/sources/cavan-2014-grabs-star-tools]]) — not a live, single-session interactive simulator.
- User-trust evidence: in the one tool with a formal user evaluation (Lahti digital twin), "Accuracy and Trust" was the lowest-scoring dimension despite strong technical model accuracy (R²=0.96), and users explicitly asked for more transparency about data sources and calculation methods ([[wiki/sources/bandaranayake-2026-lahti-digital-twin]]) — a citable argument for transparent, literature-sourced coefficients over black-box ML predictions.

## Mechanisms / How It Works
Reviewed tools cluster into three architectures:
1. **Static/screening GIS overlay tools** — pre-processed data layers a user browses and visually overlays; no live computation ([[wiki/sources/smith-2009-manchester-gis-dss]], the GRaBS Assessment Tool half of [[wiki/sources/cavan-2014-grabs-star-tools]]).
2. **Physics-based simulators, lightweight or heavyweight** — an energy-balance or CFD/mesoscale climate model computes temperature from land-cover/geometry input; either run as a quick desktop job (TARGET/UMEP, [[wiki/sources/chen-2026-umep-target]]) or requiring institutional HPC (DUCT, [[wiki/sources/aydt-2026-duct-singapore]]).
3. **ML-based digital twins** — a trained model (e.g. random forest over spectral indices) predicts outcome variables from user-specified interventions, fast but not physically or literature grounded ([[wiki/sources/bandaranayake-2026-lahti-digital-twin]]).

This project's own tool is architecturally a fourth pattern not represented in the reviewed literature: live, browser-based, parameter-adjustable simulation using **static, individually-cited literature coefficients** (not a trained model, not a full physics simulation) — trading physical completeness for speed, transparency, and reproducibility, and additionally integrating a vulnerability dimension none of the reviewed tools include.

## Evidence and Data
- [[wiki/sources/cavan-2014-grabs-star-tools]]: GRaBS Assessment Tool (350+ static layers, Google Maps-based PPGIS) + STAR Tools (Surface Temperature Tool + separate Surface Runoff Tool); Mersey Forest Plan case study (210 wards); ⭐⭐ closest prior tool.
- [[wiki/sources/smith-2009-manchester-gis-dss]]: earlier (2009) forerunner of the same Manchester lineage; explicit "no on-the-fly processing" statement.
- [[wiki/sources/aydt-2026-duct-singapore]]: heaviest-compute example (WRF+PALM-4U coupling, up to 6,144 core-hours/run); Singapore Green Plan 2030 policy-driven scenarios.
- [[wiki/sources/chen-2026-umep-target]]: lightest-compute physics-based example (energy-balance model, <1 hour desktop runtime); explicit "accessibility barrier is the interface, not the model" framing, closest to this project's own motivation.
- [[wiki/sources/bandaranayake-2026-lahti-digital-twin]]: ML-based approach; explicit user-trust evaluation gap despite high technical accuracy.

## Debates and Uncertainties
- Is "accessibility" better achieved by simplifying the underlying model (this project; TARGET/UMEP) or by keeping full physical complexity but building a better interface on top (DUCT)? The reviewed evidence suggests interface alone does not solve the compute-cost/data-availability barrier (DUCT still requires HPC and proprietary data despite a polished UI), while model-simplification approaches (TARGET/UMEP, this project) achieve genuine desktop/browser-level accessibility at the cost of physical completeness (no advection, no anthropogenic heat, simplified geometry).
- Whether a coefficient-based (literature-derived, static) tool or an ML-based tool is more trustworthy to end users is an open, only lightly evidenced question — the one available data point (Lahti) suggests technical accuracy alone does not guarantee user trust, and that transparency about *how* a number was derived matters independently.
- No reviewed tool has attempted to integrate three dimensions (heat + vulnerability + water/unsealing) simultaneously in one live interface — this is a genuine, not just incrementally narrower, gap in the reviewed literature as of 2026.

## Related Concepts
- [[wiki/concepts/heat-vulnerability-index]]
- [[wiki/concepts/land-surface-temperature]]
- [[wiki/concepts/entsiegelung]]
- [[wiki/concepts/green-infrastructure]]

## Relevant Entities
- [[wiki/entities/manchester]]
- [[wiki/entities/wuerzburg]]

## Sources
- [[wiki/sources/cavan-2014-grabs-star-tools]]
- [[wiki/sources/smith-2009-manchester-gis-dss]]
- [[wiki/sources/aydt-2026-duct-singapore]]
- [[wiki/sources/chen-2026-umep-target]]
- [[wiki/sources/bandaranayake-2026-lahti-digital-twin]]
