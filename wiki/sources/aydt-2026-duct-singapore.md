---
title: "Source: Aydt et al. 2026 — Digital Urban Climate Twin (DUCT), Singapore"
type: source
tags: [interactive-tools, digital-twin, physics-based, heavyweight, no-vulnerability, singapore]
sources: 1
updated: 2026-08-18
---

# Source: Tools to manage Singapore's heat: Coupled climate and anthropogenic heat emission models for urban comfort in a digital twin framework

- **Type:** paper
- **Author(s):** Heiko Aydt, Juan Angel Acero, Jordan Ivanchev, Ido Nevat, Ayu Sukma Adelia, Jerin Benny Chalakkal, Mathias Niffeler, Minn Lin Wong, Ander Zozaya, Kristina Orehounig
- **Date:** 2026 (received 2025-07-25, accepted 2026-01-12)
- **Venue:** *City and Environment Interactions* 29:100301, DOI 10.1016/j.cacint.2026.100301
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/1-s2.0-S2590252026000085-main.pdf` in the code project

## Summary
The Digital Urban Climate Twin (DUCT) is a joint researcher–government "Cooling Singapore 2.0" project coupling mesoscale (WRF, ~300m resolution) and microscale (PALM-4U large-eddy simulation, 5m resolution) urban climate models with anthropogenic-heat-emission models for buildings (City Energy Analyst), traffic (EMME-based), industry, and power plants, exposed through a browser-based "DUCT Explorer" interface that lets planners run pre-defined "what-if" scenarios (e.g. converting forest to high-rise, adding wind corridors, comparing centralized vs. decentralized parks) tied to Singapore's Green Plan 2030 policy targets. It is the most computationally heavy tool reviewed for this project: a 24-hour mesoscale run costs ~1,152 core-hours (48 cores × 24h), and a microscale run over a 2×2km domain costs ~6,144 core-hours (256 cores × 24h).

A demonstrated case study converts Tengah Forest (700 ha) to residential land use and shows the resulting mesoscale temperature/wind-speed deltas; a separate microscale case study shows an urban park reduces air temperature up to 1.0°C but tree-induced wind blockage can reduce wind speed by up to 2.6 m/s, illustrating a genuine trade-off the tool surfaces (shading/evapotranspiration cooling vs. reduced ventilation) that a simpler LST-only tool would miss.

## Key Claims
1. DUCT is explicitly positioned as filling two gaps in prior urban digital twins: (a) most integrate only one spatial scale (meso *or* micro) rather than coupling both, and (b) most provide visualization/description only, with "limited capability for nonexpert users... to configure and run their own simulations and explore alternative scenarios" — this second gap is the same accessibility gap this project's paper targets, but DUCT's own answer to it (a browser UI wrapping HPC-scale physics models) requires institutional compute infrastructure (national supercomputing center, cloud clusters) that a reproducible open-data mid-city tool cannot assume.
2. No social-vulnerability, demographic, or equity dimension is modeled anywhere in DUCT — its scenario set is entirely physical/infrastructural (land use, vehicle fleet, vegetation fraction, cooling technology).
3. The system requires substantial agency-level data-sharing coordination (multiple Singapore government agencies contributed proprietary datasets) and is explicitly stated as not portable to another city without re-collecting/re-deriving a comparable dataset — contrasts with this project's fully open-data (OSM, Zensus, Copernicus/Landsat, Bavarian ATKIS) reproducibility.
4. Physical trade-offs invisible to LST-only models are surfaced: tree cover improves thermal comfort (PET) but reduces wind speed, occasionally *worsening* comfort in wind-dependent tropical contexts — a reminder that coefficient-based cooling estimates (like this project's) simplify away second-order physical interactions that a full microscale model would capture.
5. The paper explicitly names computational cost as a standing limitation and proposes ML surrogate/emulator models as future work to enable faster, more accessible scenario testing — implicitly conceding the same speed/accessibility trade-off this project resolves by using literature-derived static coefficients instead of live physics simulation.
6. Performance validation reported: mesoscale RMSE 1.56°C (2m temperature), microscale RMSE 0.44–0.69°C — the microscale model is more accurate but is the more computationally expensive of the two by roughly 5×.

## Data and Figures
- Mesoscale (WRF): ~300×300m resolution, RMSE 1.56°C (2m temp), 8.12% RH, ~1,152 core-hours/24h run.
- Microscale (PALM-4U): 5m resolution, RMSE 0.44–0.69°C (2m temp), ~6,144 core-hours per 2×2km domain/24h run.
- Case study: Tengah Forest (700 ha) → residential conversion; urban park scenario shows up to −1.0°C air temp but up to −2.6 m/s wind speed with heavy tree cover; PET improves by up to 10°C in park areas in some locations, worsens in others due to reduced wind.

## Contradictions / Gaps
- No vulnerability dimension — supports the gap statement by omission, consistent across all Cluster 4 sources.
- Heaviest-compute tool in the whole comparison set — the single strongest "expert/heavyweight" pole for positioning this project's lightweight, coefficient-based, browser-only tool against.
- Not reproducible outside Singapore without equivalent proprietary agency data — a second, distinct axis of contrast (openness/reproducibility) beyond just compute cost, worth naming separately from the Lahti/UMEP-TARGET "lightweight but still expert-only" contrasts.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/interactive-climate-tools]] (new)
- [[wiki/index]]
