---
title: "Source: Bandaranayake et al. 2026 — Digital Twin for UHI Mitigation, Lahti"
type: source
tags: [interactive-tools, digital-twin, machine-learning, lst-only, no-vulnerability, finland]
sources: 1
updated: 2026-08-18
---

# Source: A Digital Twin-Based System to Support Urban Planners in Mitigating the Urban Heat Island Effect

- **Type:** paper (design science research)
- **Author(s):** Iresha Bandaranayake, Dominik Siemon, Ram Gurung (LUT University, Lappeenranta, Finland)
- **Date:** 2026
- **Venue:** DESRIST 2026 (International Conference on Design Science Research in Information Systems and Technology), LNCS vol. 16606, pp. 43–58, DOI 10.1007/978-3-032-28313-9_3
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/978-3-032-28313-9_3.pdf` in the code project
- ⚠️ Note: an earlier project handoff note described this as a "Padua" case study — the actual case study city is **Lahti, Finland**. Verify city name when drafting.

## Summary
A design-science-research (eDSR methodology) digital twin for the city of Lahti, Finland, letting urban planners add hypothetical interventions — tree areas, buildings, water bodies, green roofs — to a 3D CesiumJS visualization of the city and immediately see a forecast of the resulting land-surface-temperature (LST) change. Under the hood, a random-forest ML model (trained on Sentinel-2/Landsat-9-derived spectral indices — NDVI, NDWI, NDBI — plus geographic coordinates) predicts LST for each 30m grid cell; user interventions are translated into a new spectral-band mixture per cell (weighted blend of the object's known reflectance and the original pixel's reflectance, by intervention coverage fraction), and the retrained model then predicts the new LST for that mixture. The system was evaluated with 5 domain experts (environmental specialist, urban planners, sustainable-planning students) via a structured questionnaire.

The ML model itself performs well after tuning (R²=0.96, RMSE=1.16°C after adding coordinate features), but the *user* evaluation surfaced a persistent trust gap: "Accuracy and Trust" scored the lowest of all evaluated dimensions (mean 3.70/5), and participants explicitly asked for more transparency about data sources and calculation methods even though they found the intervention outcomes broadly consistent with real-world expectations.

## Key Claims
1. The tool is explicitly LST-only — no social-vulnerability, demographic, or equity dimension is modeled or visualized at any point; the design objectives (integration of environmental/spatial/temperature data, ML forecasting, 3D visualization, usability) contain no vulnerability component.
2. The prediction mechanism is a black-box ML model (random forest over spectral indices), not a literature-derived physical coefficient — contrasts with this project's fully sourced, per-coefficient-citable simulation approach (`simulation_params.py`).
3. Despite technically strong predictive accuracy (R²=0.96), user trust in the predictions was the weakest-rated dimension in the evaluation — the authors explicitly conclude that "predictive performance alone does not ensure decision support value" and that transparency about inputs/computation is a core design requirement, not a secondary feature, for climate-decision tools aimed at practitioners.
4. Four intervention types are supported (trees, buildings, water, green roofs), each parameterized via *averaged, generic* spectral-reflectance values from the ECOSTRESS Spectral Library — not species-specific or locally calibrated coefficients (contrast with this project's Würzburg-specific, allometrically-derived tree-cooling coefficients).
5. The tool positions itself explicitly against "descriptive" GIS-based UHI mapping tools (citing prior work that communicates indicators via static 2D maps) and against heavyweight CFD/mesoscale physics models (ENVI-met, PALM-4U, WRF) as too expert-only for rapid scenario testing — the same "accessibility vs. expertise" framing this project's paper should make.
6. Future work explicitly named: adding more tree/building material types, adding roads/green corridors as intervention options, and improving the ML model's generalizability to noisier cities than Lahti.

## Data and Figures
- ML model final performance (after retraining with coordinates): R²=0.96, RMSE=1.16°C, MAE=0.85°C, Pearson r=0.98.
- User evaluation (n=5, closed-ended questions, 1–5 scale): Ease of Use 3.92, Visualization Clarity 3.90, Usefulness 4.12, Decision Support/Intention to Use 3.95, **Accuracy and Trust 3.70 (lowest)**, Overall Reflection 4.33.
- Data sources: Sentinel-2 (2021–2025 summer, NDVI/NDWI/NDBI/EVI), Landsat 9 (LST), 30m×30m grid cells.

## Contradictions / Gaps
- ML black-box prediction vs. this project's transparent, literature-cited coefficient approach — directly usable as the "accessible but not reproducible/citable" contrast point in the paper's Related Work.
- No vulnerability, no water/unsealing dimension — supports the gap statement by omission, consistent with all Cluster 4 sources reviewed.
- The explicit finding that user trust lags technical accuracy is a citable argument *for* this project's design choice (every coefficient traceable to a cited source) as a trust-building mechanism, not just a scientific-rigor nicety.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/interactive-climate-tools]] (new)
- [[wiki/index]]
