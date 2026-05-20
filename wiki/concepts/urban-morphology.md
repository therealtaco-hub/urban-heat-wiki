---
title: "Urban Morphology"
type: concept
tags: [urban-morphology, building-density, sky-view-factor, street-canyon, lcz]
sources: 2
updated: 2026-05-20
---

# Urban Morphology

The physical form and structure of the urban environment — building heights, densities, street widths, open space ratios — as distinct from land cover (what the surface is made of). Urban morphology shapes UHI through its effect on radiation trapping, airflow, and shadow patterns.

## Key Facts

- **Building density > 20%** produces a warming effect in summer/autumn; threshold rises to > 40% in spring/winter. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*
- **Sky view factor (SVF)**: the fraction of sky visible from a point. Low SVF = deep urban canyon = trapped longwave radiation. Effect is scale-dependent: SVF inhibits LST at block scale but promotes it at grid scale. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*
- **3D morphology** (building height, volume, orientation) can be inferred from satellite imagery + GIS and used as WRF model input. *(Source: [[wiki/sources/muhammad-2021-urban-morphology-uhi]])*
- LST is **higher in central areas** in summer/autumn (dense morphology + high impervious cover); pattern reverses in spring/winter. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*

## Mechanisms / How It Works

- Dense urban canyons trap incoming solar radiation → high daytime LST
- Low SVF traps outgoing longwave radiation at night → slows nocturnal cooling
- High building density + low vegetation = low pervious surface fraction = minimal ET

## Relevance to Würzburg Project

Urban morphology data (from Würzburg's GIS, building footprints, DSM) feeds into:
1. LCZ classification → WRF simulation input
2. Identification of which street blocks have highest cooling deficit
3. Spatial targeting of greening interventions

## Related Concepts

- [[wiki/concepts/local-climate-zones]] — morphology-based classification
- [[wiki/concepts/land-surface-temperature]] — key outcome
- [[wiki/concepts/impervious-surface]] — closely linked land cover variable

## Sources

- [[wiki/sources/li-et-al-urban-form-lst-xgboost]]
- [[wiki/sources/muhammad-2021-urban-morphology-uhi]]
