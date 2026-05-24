---
title: "NDVI — Normalized Difference Vegetation Index"
type: concept
tags: [ndvi, remote-sensing, vegetation, lst-correlate, landsat]
sources: 2
updated: 2026-05-20
---

# NDVI — Normalized Difference Vegetation Index

A spectral index calculated from near-infrared (NIR) and red band reflectance: `NDVI = (NIR − Red) / (NIR + Red)`. Values range from −1 to +1; urban vegetation typically 0.2–0.6, dense forest 0.6–0.9. The standard remote sensing proxy for vegetation density and health.

## Key Facts

- **NDVI negatively correlates with LST**: higher vegetation density → lower surface temperature. *(Source: [[wiki/sources/reta-roba-hawassa-vegetation-lst]], [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*
- **Threshold for meaningful cooling: NDVI > 0.4**. Below this, vegetation has minimal impact on LST. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*
- **NDBI (built-up index) is a stronger LST predictor than NDVI** in at least one study (Hawassa City). *(Source: [[wiki/sources/reta-roba-hawassa-vegetation-lst]])*
- NDVI is a proxy for total vegetation cover, not specifically tree canopy — grass and shrubs contribute. For tree-specific analysis, individual tree crown mapping (as in García de León et al.) gives better precision.

## Mechanisms / How It Works

- Healthy green vegetation absorbs red light for photosynthesis and strongly reflects NIR → high NDVI
- Bare soil, impervious surfaces, stressed vegetation → low NDVI
- High NDVI zones have more leaf area for shade and transpiration → lower LST
- NDVI generally remains **low in all seasons except summer** in Central European cities. *(Source: [[wiki/sources/li-et-al-urban-form-lst-xgboost]])*

## Evidence and Data

| Finding | Value | Source |
|---------|-------|--------|
| LST-NDVI relationship | Negative correlation | [[wiki/sources/reta-roba-hawassa-vegetation-lst]] |
| NDVI bivariate R² with LST (Košice) | 0.63 (strongest single predictor) | [[wiki/sources/onacillova-2022-lst-downscaling]] |
| NDBI bivariate R² with LST (Košice) | 0.503 | [[wiki/sources/onacillova-2022-lst-downscaling]] |
| NDWI bivariate R² with LST (Košice) | 0.564 | [[wiki/sources/onacillova-2022-lst-downscaling]] |
| NDVI cooling threshold | > 0.4 | [[wiki/sources/li-et-al-urban-form-lst-xgboost]] |
| NDBI vs. NDVI as LST predictor | NDBI stronger (Hawassa); NDVI stronger (Košice) | [[wiki/sources/reta-roba-hawassa-vegetation-lst]], [[wiki/sources/onacillova-2022-lst-downscaling]] |

## Debates and Uncertainties

- The NDVI > 0.4 cooling threshold is derived from Chinese cities — may not apply directly to Würzburg.
- NDVI conflates trees with grass and other low vegetation; tree canopy percentage is a more precise variable for cooling quantification.
- Seasonal variation: NDVI is low in winter even in areas with dense deciduous tree cover — seasonal stratification needed.

## Related Concepts

- [[wiki/concepts/land-surface-temperature]] — primary correlate
- [[wiki/concepts/remote-sensing-methods]] — calculation from Landsat bands
- [[wiki/concepts/green-infrastructure]] — what NDVI measures
- [[wiki/concepts/impervious-surface]] — inverse relationship via NDBI

## Sources

- [[wiki/sources/reta-roba-hawassa-vegetation-lst]]
- [[wiki/sources/li-et-al-urban-form-lst-xgboost]]
