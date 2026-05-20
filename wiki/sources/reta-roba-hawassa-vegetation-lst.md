---
title: "Source: Geospatial analysis of vegetation and land surface temperature for urban heat island mitigation in Hawassa City, Ethiopia"
type: source
tags: [lst, ndvi, ndbi, vegetation, landsat, hawassa, sub-saharan, remote-sensing, time-series]
sources: 1
updated: 2026-05-20
---

# Source: Reta-Roba & Worku-Tabor — Vegetation and LST in Hawassa City

- **Type:** Peer-reviewed research article
- **Authors:** Zenebe Reta-Roba (Mattu University, Ethiopia), Kenate Worku-Tabor
- **Study city:** Hawassa City, Ethiopia
- **Period:** 1991–2021 (three Landsat scenes: Landsat 5 TM 1991, Landsat 7 ETM+ 2005, Landsat 8 OLI 2021)
- **Raw file:** [[raw/Geospatial analysis of vegetation.pdf]]

## Summary

This study examines a 30-year trajectory of vegetation loss and LST increase in Hawassa City using multi-temporal Landsat analysis. It demonstrates the negative correlation between NDVI and LST and positive correlation between NDBI (built-up index) and LST, finding that NDBI is a more effective predictor of LST than NDVI. It also quantifies the cooling effect of water bodies.

The study is geographically distant from Würzburg (sub-Saharan Africa), but methodologically relevant: its approach of correlating Landsat-derived LST, NDVI, and NDBI over time using mono-window algorithm retrieval is a direct analogue to what the user's project aims to do for Würzburg.

## Key Claims

1. **Negative correlation between LST and NDVI** — higher vegetation → lower surface temperature.
2. **Positive correlation between LST and NDBI** — more built-up area → higher surface temperature.
3. **NDBI is a more effective predictor of LST than NDVI** in this study.
4. Built-up area increased by **+23.2%** (1991–2021); sparse vegetation declined by 19.3%.
5. **Water bodies reduce maximum temperature** by 2.1°C (1991), 1.2°C (2005), 0.5°C (2021) — declining effectiveness as urban context changes.
6. Mono-window algorithm used for LST retrieval from Landsat thermal bands.
7. Long-term: urban expansion at expense of vegetated areas directly increased LST.

## Data and Figures

| Land cover change (1991–2021) | Delta |
|-------------------------------|-------|
| Dense vegetation | −1.6% |
| Sparse vegetation | −19.3% |
| Built-up area | +23.2% |

| Water body cooling effect | Year | ΔT max |
|--------------------------|------|--------|
| 1991 | 2.1°C | |
| 2005 | 1.2°C | |
| 2021 | 0.5°C | |

## Contradictions / Gaps

- Sub-Saharan African city — climate, vegetation types, and urban form differ significantly from Central European cities.
- The declining water body cooling effect over time is unexplained — may relate to changed surrounding land use.
- NDBI as better predictor than NDVI is an interesting finding, but may not hold in all contexts.

## Wiki Pages Updated

- [[wiki/sources/reta-roba-hawassa-vegetation-lst]] ← this page
- [[wiki/concepts/land-surface-temperature]]
- [[wiki/concepts/ndvi]]
- [[wiki/concepts/remote-sensing-methods]]
- [[wiki/concepts/impervious-surface]]
