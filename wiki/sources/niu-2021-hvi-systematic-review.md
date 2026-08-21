---
title: "Source: Niu et al. 2021 — Systematic Review of HVI Development and Validation"
type: source
tags: [vulnerability, hvi, systematic-review, pca, methodology]
sources: 1
updated: 2026-08-18
---

# Source: A Systematic Review of the Development and Validation of the Heat Vulnerability Index: Major Factors, Methods, and Spatial Units

- **Type:** paper (systematic review, PRISMA methodology)
- **Author(s):** Yanlin Niu, Zhichao Li, Yuan Gao, Xiaobo Liu, Lei Xu, Sotiris Vardoulakis, Yujuan Yue, Jun Wang, Qiyong Liu
- **Date:** 2021 (accepted 2021-03-29, published online 2021-04-27)
- **Venue:** *Current Climate Change Reports* 7:87–97, DOI 10.1007/s40641-021-00173-3
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/40641_2021_Article_173.pdf` in the code project
- ⚠️ Note: an earlier project handoff note mislabeled this as "Cheng et al. 2021" — the correct authors are **Niu et al.**; verify against the DOI above when drafting citations.

## Summary
A PRISMA-guided systematic review of 13 published Heat Vulnerability Index (HVI) studies (out of 46 total HVI papers found 2010–2020) that were validated against observed health outcome data. The review catalogs, across all 13 studies: which factor categories were used (hazard exposure, demographic characteristics, socioeconomic conditions, built environment, underlying health), which spatial unit was chosen (census tract, postal code, administrative area, or regular grid), which development method was applied (PCA/factor analysis in 11 of 13 studies; regression or data-driven approaches in the rest), and which validation method and health outcome (almost always mortality) was used.

The review's central finding is a caution rather than an endorsement: even though a higher HVI is usually associated with worse health outcomes across the reviewed studies, the strength of that association is consistently weak (e.g. R²≈0.03 in one Dallas study), and PCA-derived index components are hard to interpret and are highly sensitive to the input-variable set and study area — the review explicitly recommends more transparent, better-validated approaches going forward, and flags that governance/institutional-capacity factors are almost never included despite theoretical relevance.

## Key Claims
1. Across the 13 reviewed HVI studies, demographic characteristics, socioeconomic conditions, and built-environment factors are used far more often than hazard-exposure or underlying-health factors — hazard exposure appears in only 5 of 13 studies, meaning most published HVIs under-weight the actual heat magnitude relative to social vulnerability.
2. PCA/factor analysis is the dominant HVI construction method (11 of 13), but the review explicitly notes PCA components are "not as readable and interpretable as original features" once extracted, and that different input-variable sets or spatial scales produce different, non-comparable results (citing Tate 2012's uncertainty/sensitivity analysis of vulnerability-index designs).
3. Spatial units vary widely (census tract in 8/13 studies, postal code, administrative county, and — in one case (He et al. 2019, Shanghai) — a 500m regular grid, the closest spatial-unit precedent in this review set to this project's 100m Zensus grid).
4. Validation against mortality data shows generally weak statistical association (R² as low as 0.03 in Mallen et al.'s Dallas HVI; Conlon et al.'s supervised/unsupervised PCA HVIs also showed "very low R²"), which the review interprets as HVIs "should be used with caution for identifying vulnerable areas" rather than treated as precise predictors.
5. No reviewed study includes a governance/institutional-capacity factor, despite theoretical calls for one (Zhang et al., Beijing) — flagged as a gap for future HVI development.
6. The review explicitly recommends more open/available health data at fine spatial resolution to enable proper validation, and highlights that duration and location diversity of validation data (not just sample size) determines HVI reliability.

## Data and Figures
- 941 initial records (686 English + 255 Chinese) → 13 included studies after PRISMA screening.
- Factor usage across studies: social cohesion 15%, race/ethnicity 13%, landscape (land cover) 12%, age 10%, economic status 10% — the five most-used factors overall.
- 9 of 13 US-based, 4 non-US (UK, Canada, China, Korea).
- Sample sizes for validation ranged 159–4,765 spatial units; validation duration ranged 1–17 years (average 8).

## Contradictions / Gaps
- This review's finding that PCA-derived indices are hard to interpret and unstable across input sets directly supports this project's choice of a transparent, literature-fixed weighted-sum HVI (0.6 LST / 0.4 elderly share) over a PCA-derived index — worth citing explicitly as justification in Methods.
- The review's caution about weak HVI–mortality correlation is a caveat this project should acknowledge (no local health-outcome validation exists for the Würzburg HVI either) rather than a claim to build on.
- None of the 13 reviewed studies apply Bayesian/empirical-Bayes shrinkage for small-population units — again, a methodological point of differentiation for this project's `shrink_senior_rate()`.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/heat-vulnerability-index]] (new)
- [[wiki/index]]
