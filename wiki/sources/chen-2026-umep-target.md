---
title: "Source: Chen et al. 2026 — UMEP-TARGET QGIS Interface"
type: source
tags: [interactive-tools, physics-based, lightweight, gis-plugin, no-vulnerability, zurich, switzerland]
sources: 1
updated: 2026-08-18
---

# Source: An open-source GIS user interface for the TARGET climate model in the Urban Multi-scale Environmental Predictor (UMEP) tool

- **Type:** paper
- **Author(s):** Jixuan Chen, Peter M. Bach, Matthias Demuzere, João P. Leitão, Fredrik Lindberg, Kerry A. Nice, Nils Wallenberg
- **Date:** 2026 (received 2025-11-07, accepted 2026-05-24)
- **Venue:** *Environmental Modelling & Software* 203:107043, DOI 10.1016/j.envsoft.2026.107043
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/1-s2.0-S1364815226001908-main.pdf` in the code project

## Summary
TARGET (the Air-temperature Response to Green/blue-infrastructure Evaluation Tool, Broadbent et al. 2019) is a physically-based but computationally efficient urban energy-balance model: it partitions net radiation into sensible/latent/ground-storage heat fluxes per land-cover type (roofs, pavement, dry/irrigated grass, trees, water) within a simplified urban-canyon geometry, and aggregates to canyon-average surface and 2m air temperature per grid cell (recommended 100m for air temperature, 30m for surface temperature). Until this paper, TARGET was only usable via Java/Python code, restricting it to a small expert community. This paper adds a full point-and-click interface inside UMEP (Urban Multi-scale Environmental Predictor), an existing open-source QGIS plugin, covering the entire workflow — land-cover fraction preparation, building-morphology derivation from DSM/DEM, meteorological-forcing preparation (local stations or ERA5), simulation execution, and spatial/temporal output visualization — all inside QGIS.

A Zurich case study (28.8 km² domain, 100m simulation grid, a 4-day July 2023 heatwave) demonstrates the full workflow: baseline hotspot identification, then three green/blue-infrastructure intervention scenarios (irrigated-grass greening, tree-cover expansion, water features) each re-run and compared. Tree cover expansion was the most effective, reducing hotspot cell count by 83% (125→21 cells) with a mean air-temperature reduction of −0.60°C (up to −1.6°C in the most severe cells); greening/irrigation achieved 57% hotspot reduction; water features only 46%.

## Key Claims
1. TARGET/UMEP is explicitly positioned in the "accessibility gap" between heavyweight CFD/mesoscale models (ENVI-met, PALM-4U, WRF — accurate but requiring HPC resources and specialist expertise) and no physically-based tool at all: "a major barrier is therefore not the availability of suitable models, but rather the absence of user-friendly interfaces" — nearly verbatim the same framing this project's own paper should use for its novelty claim.
2. Despite the accessibility framing, the tool still requires GIS software (QGIS) and substantial expert data preparation: high-resolution Digital Surface/Elevation Models, official land-cover classification rasters, and meteorological forcing data (radiation, humidity, wind, pressure) — a genuinely lower barrier than coding TARGET by hand, but still far from a public no-install web app a citizen or non-GIS planner could use directly.
3. No social-vulnerability, demographic, or equity dimension exists in TARGET/UMEP at all — purely a physical land-cover/temperature model; the paper's own "positioning among planning support tools" section explicitly compares itself only against other physical microclimate models (ENVI-met, SUEWS, UWG, UrbanBEATS), never against any vulnerability- or equity-integrating tool.
4. TARGET has known physical simplifications by design: no horizontal advection, no anthropogenic heat fluxes, simplified canyon geometry, no vertical vegetation structure — explicitly traded off for computational speed (a full 4-day Zurich simulation completed in under an hour on a standard desktop).
5. The paper explicitly frames UMEP-TARGET as "best seen as a complementary first-order screening tool" whose outputs guide *where* more detailed, expensive modeling should subsequently focus — an explicit acknowledgment that fast/lightweight and physically-precise are in tension, and that fast-first-pass tools have a distinct, legitimate role rather than needing to compete head-on with heavyweight models.
6. Land-cover intervention scenarios in the case study are idealized 100% replacements within pre-identified hotspot cells (not partial/realistic replacement fractions), and the authors explicitly caution that resulting cooling magnitudes are "upper bounds" given real-world physical/financial/institutional constraints on how much land cover can actually change — directly analogous to this project's own `TYPICAL_REALIZATION_RATE` caveat for entsiegelung.

## Data and Figures
- Zurich case study: 28.8 km² domain, 100m grid, 4-day July 2023 heatwave (06–09 July, 1 day spin-up).
- Tree-cover-expansion scenario: 125→21 hotspot cells (83% reduction), mean ΔT −0.60°C (range −0.06 to −1.60°C).
- Greening/irrigation: 57% hotspot reduction, mean ΔT −0.27°C.
- Water features: 46% hotspot reduction, mean ΔT −0.19°C (least effective of the three).
- Full 4-day simulation runtime: <1 hour on a standard desktop computer (vs. thousands of core-hours for DUCT's microscale runs — see [[wiki/sources/aydt-2026-duct-singapore]]).

## Contradictions / Gaps
- No vulnerability dimension — consistent with all Cluster 4 sources; strongest and most directly comparable "lightweight but still expert/GIS-only, still no equity dimension" contrast in the whole set, given its explicit "lower the barrier to entry" framing mirrors this project's own motivation almost exactly.
- Still requires QGIS installation, DSM/DEM acquisition, and land-cover reclassification by the user — a genuine but partial accessibility improvement, useful as the "closest attempt, but still short of a public web tool" comparison point.
- Findings (tree > greening > water for cooling effectiveness) broadly agree with this project's own coefficient ranking (tree canopy −0.069 to −0.083°C/% vs. unsealing −0.03°C/%) — worth an explicit cross-check/corroboration note in Methods or Discussion, since it's an independent physics-based confirmation of the same qualitative ordering this project's literature-derived coefficients imply.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/interactive-climate-tools]] (new)
- [[wiki/concepts/green-infrastructure]]
- [[wiki/index]]
