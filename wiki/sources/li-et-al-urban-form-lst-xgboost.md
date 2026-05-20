---
title: "Source: Investigating the effect of urban form on land surface temperature at block and grid scales based on XGBoost-SHAP"
type: source
tags: [lst, urban-form, xgboost, shap, ndvi, lcz, local-climate-zones, building-density, machine-learning]
sources: 1
updated: 2026-05-20
---

# Source: Li et al. — Urban Form and LST (XGBoost-SHAP)

- **Type:** Peer-reviewed research article
- **Authors:** Hongfei Li, Jun Yang, Jiaxing Xin, Wenbo Yu, Jiayi Ren, Huisheng Yu, Xiangming Xiao, Jianhong (Cecilia) Xia
- **Institutions:** Northeastern University (Shenyang, China); Liaoning Normal University; University of Oklahoma; Curtin University (Australia)
- **Study area:** Chinese cities
- **Raw file:** [[raw/Investigating the effect of urban form on land surface temperature at block.pdf]]

## Summary

This study uses eXtreme Gradient Boosting (XGBoost) combined with SHapley Additive exPlanations (SHAP) to identify the most important urban form factors driving LST, and to detect non-linear thresholds in their effects. It operates at both block-level and grid-level scales within Local Climate Zone (LCZ) classifications.

Key methodological contribution: SHAP values make the machine learning model interpretable — revealing not just *which* factors matter but *at what values* they flip from cooling to warming or vice versa. This is a relevant methodological reference for the simulation component of the Würzburg project.

## Key Claims

1. **NDVI must exceed 0.4** for significant cooling effect — below this threshold, vegetation has minimal LST impact.
2. **Shannon's Diversity Index (SHDI) > 0.65** produces a cooling effect; below this threshold, urban form diversity is insufficient to reduce LST.
3. **Building density > 20% (summer/autumn) or > 40% (spring/winter)** produces a warming effect.
4. **NDBI, NDVI, and SHDI** are the main contributors to LST variation.
5. **Sky view factor** inhibits LST at block scale but *promotes* LST at grid scale — a scale-dependent reversal.
6. **Summer effect is strongest**: Summer > Spring > Autumn > Winter.
7. LST is higher in central areas than peripheral ones in summer/autumn; reversed in spring/winter.
8. LCZ classification enables comparison across different urban morphologies.
9. Heat-related deaths among people >65 years have risen **85% globally since 1990** (cites Romanello et al., Lancet).

## Data and Figures

| Urban Factor | LST Effect | Threshold |
|-------------|-----------|-----------|
| NDVI | Cooling | must exceed 0.4 for significant effect |
| SHDI | Cooling when high | > 0.65 |
| Building density | Warming when high | > 20% (summer), > 40% (spring) |
| NDBI | Warming | positive correlation |
| Sky view factor | Scale-dependent | inhibits at block, promotes at grid |

## Contradictions / Gaps

- Study is Chinese cities — urban form, climate, and vegetation cover differ from Central European context.
- NDVI threshold of 0.4 is derived from this specific context; threshold may differ in Würzburg.
- Machine learning models may not generalize well outside their training region.

## Wiki Pages Updated

- [[wiki/sources/li-et-al-urban-form-lst-xgboost]] ← this page
- [[wiki/concepts/land-surface-temperature]]
- [[wiki/concepts/ndvi]]
- [[wiki/concepts/local-climate-zones]]
- [[wiki/concepts/urban-morphology]]
- [[wiki/concepts/impervious-surface]]
