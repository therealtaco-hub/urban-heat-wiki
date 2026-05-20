---
title: "Local Climate Zones (LCZ)"
type: concept
tags: [lcz, urban-morphology, wrf, classification, simulation]
sources: 2
updated: 2026-05-20
---

# Local Climate Zones (LCZ)

A classification scheme that divides urban and rural areas into 17 standardised zone types based on physical properties: surface cover, fabric, structure, and human activity. Originally proposed by Stewart & Oke (2012) as a universal framework for urban climate studies. Increasingly used as the land use input for mesoscale UHI simulation models like WRF.

## Key Facts

- 17 classes: 10 urban (e.g., compact high-rise, open low-rise, heavy industry, large low-rise) + 7 rural (e.g., dense forest, scattered trees, low plants, water).
- Designed to replace ad-hoc, city-specific land use classifications — enables cross-city comparison.
- **WRF default LULC datasets (MODIS) are too coarse for city-scale UHI simulation** — LCZ maps provide finer resolution and more meaningful urban class distinctions. *(Source: [[wiki/sources/muhammad-2021-urban-morphology-uhi]])*
- WUDAPT (World Urban Database and Access Portal Tools) provides a community platform for generating and sharing LCZ maps globally.
- GIS-based LCZ derivation (using CityGML, building footprints, etc.) outperforms WUDAPT in areas with good GIS data. *(Source: [[wiki/sources/muhammad-2021-urban-morphology-uhi]])*
- Used by Li et al. to stratify LST analysis across different urban morphology types. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*

## Mechanisms / How It Works

Each LCZ is defined by quantitative ranges for:
- Sky view factor (SVF)
- Aspect ratio (building height / street width)
- Building surface fraction
- Impervious surface fraction
- Pervious surface fraction
- Height of roughness elements (building height)
- Terrain roughness class

These properties collectively determine how much solar radiation reaches surfaces, how much longwave radiation is trapped, and how much convective cooling occurs.

## Relevance to Würzburg Project

LCZ maps are the key link between urban morphology data and UHI simulation:
1. Derive LCZ map for Würzburg from available GIS data (building footprints, land use, tree data)
2. Use LCZ map as input for WRF or similar model
3. Simulate counterfactual scenarios: modify LCZ class of specific zones (e.g., change "compact low-rise" to "open low-rise with trees") and model temperature impact

## Related Concepts

- [[wiki/concepts/urban-morphology]] — LCZ is one way to characterise morphology
- [[wiki/concepts/land-surface-temperature]] — what LCZ simulation predicts
- [[wiki/concepts/urban-heat-island]] — what LCZ helps model

## Relevant Entities

- [[wiki/entities/tu-muenchen]] — Muhammad thesis uses LCZ+WRF
- [[wiki/entities/wuerzburg]] — target city for LCZ-based simulation

## Sources

- [[wiki/sources/muhammad-2021-urban-morphology-uhi]]
- [[wiki/sources/li-et-al-urban-form-lst-xgboost]]
