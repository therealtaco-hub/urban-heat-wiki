---
title: "Source: The Relation of Land Surface Temperature and Trees across Different Urban Land Use Classes based on Remote Sensing"
type: source
tags: [lst, trees, land-use, munich, remote-sensing, würzburg, dlr, regression, key-source]
sources: 1
updated: 2026-05-20
---

# Source: García de León et al. — LST and Trees across Land Use Classes (Munich)

- **Type:** Conference/journal paper (IEEE)
- **Authors:** Andrea Sofía García de León, Tobias Leichtle (DLR), Tobias Ullmann, Antonio Castañeda-Gómez, Thomas Rötzer (TUM), Nils Karges, Klaus Martin (SLU), Hannes Taubenböck (DLR/Univ. Würzburg) — all Univ. Würzburg or DLR
- **Downloaded:** 2026-05-20 (via Technische Hochschule Würzburg-Schweinfurt access)
- **Study city:** Munich, Germany
- **Raw file:** [[raw/The_Relation_of_Land_Surface_Temperature_and_Trees_across_Different_Urban_Land_Use_Classes_based_on_Remote_Sensing.pdf]]

## Summary

This study directly quantifies the relationship between land surface temperature (LST) and urban tree canopy cover across five land use classes in Munich. The authors combine a downscaled high-resolution LST product (summer 2020) with individual-tree crown data from segmentation of aerial imagery (>166,000 trees) and land use polygons from the ATKIS dataset. Using linear regression on 8,584 land use polygons, they establish that LST decreases consistently as tree canopy cover increases — across every land use class studied.

The headline finding: **each 1% increase in tree canopy cover is associated with a mean LST decrease of approximately 0.069°C** across the whole study area. Land use class matters significantly: the cooling coefficient is steeper in Mixed and Residential areas (–0.083°C/%) than in Recreational areas (–0.038°C/%), where baseline canopy cover is already high and LST is already lower.

This is the most directly applicable paper to the user's Würzburg project — it was produced by Würzburg and DLR researchers, uses the same general methodology (remote sensing LST + individual tree data + land use), and establishes the quantitative LST–tree relationship that underpins the simulation goal.

## Key Claims

1. Each **1% increase in tree canopy cover → −0.069°C mean LST** (whole study area, Munich summer 2020).
2. Relationship is **negative and consistent across all five land use classes**.
3. **Recreational areas** (parks, forests): lowest LST (median ~34.5°C), highest canopy cover (~65% median), shallowest slope (−0.038°C/%).
4. **Mixed areas**: highest LST (median ~39°C), lowest canopy cover (~10% median), steepest slope (−0.083°C/%).
5. **Industrial, Traffic, Residential**: LST median ~38°C, canopy cover median <25%.
6. R² values: 0.41 (Recreational) to 0.61 (Traffic) — moderate to strong fit.
7. **>166,000 individual tree crowns** mapped from high-res aerial imagery for Munich's central area.
8. Data: downscaled LST product (summer June–September 2020), ATKIS land use polygons.

## Data and Figures

| Land Use Class | LST Median | Canopy Cover Median | Regression Coeff. (°C/%) | R² |
|----------------|-----------|---------------------|--------------------------|-----|
| Mixed | ~39°C | ~10% | −0.083 | n/a |
| Residential | ~38°C | <25% | −0.083 | n/a |
| Industrial | ~38°C | <25% | n/a | n/a |
| Traffic | ~38°C | <25% | n/a | 0.61 |
| Recreational | ~34.5°C | ~65% | −0.038 | 0.41 |
| **Whole area** | — | — | **−0.069** | high |

## Contradictions / Gaps

- Study is for Munich (summer 2020); direct transfer to Würzburg requires validation with Würzburg-specific data.
- Exact regression coefficients for Industrial and Traffic classes not fully extracted — raw PDF needed for table.
- Single-year snapshot (2020); temporal trends not addressed.
- Air temperature effects not measured — LST only.

## Wiki Pages Updated

- [[wiki/sources/garcia-de-leon-lst-trees-munich]] ← this page
- [[wiki/concepts/land-surface-temperature]]
- [[wiki/concepts/green-infrastructure]]
- [[wiki/concepts/remote-sensing-methods]]
- [[wiki/entities/wuerzburg]]
- [[wiki/entities/university-of-wuerzburg]]
- [[wiki/entities/dlr]]
- [[wiki/entities/muenchen]]
- [[wiki/entities/thomas-roetzer]]
