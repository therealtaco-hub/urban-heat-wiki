---
title: "Source: Gray et al. 2021 — Predicting Canopy Cover from Individual Tree Measurements"
type: source
tags: [canopy-cover, crown-overlap, beer-lambert, crookston-stage, forest-inventory, methodology, simulation]
sources: 1
updated: 2026-06-19
---

# Source: Predicting Canopy Cover of Diverse Forest Types from Individual Tree Measurements

- **Type:** journal article
- **Author(s):** Andrew N. Gray, Anne C.S. McIntosh, Steven L. Garman, Michael A. Shettles
- **Date:** 2021
- **Journal:** Forest Ecology and Management 501 (2021) 119682
- **DOI:** https://doi.org/10.1016/j.foreco.2021.119682
- **Raw file:** [[raw/Predicting canopy cover of diverse forest types from individual.pdf]]

## Summary

Gray et al. evaluated three approaches to estimate stand-level canopy cover from standard forest inventory tree measurements across 1,706 inventory plots representing diverse forest types in Oregon, USA. The study compares: (1) adjusted crown-width summation methods, (2) adjusted Beer-Lambert crown overlap correction factors, and (3) statistical models from stand-level attributes.

This source is primarily relevant as an **empirical validation and limitation analysis of the Crookston & Stage (1999) random crown overlap formula** — the same model used in the *Resilientes Würzburg* `/api/simulate/baeume` endpoint:

```
C_olap = 100 × (1 − exp(−0.01 × C_raw))
```

Gray et al. confirm the formula is methodologically sound for low-to-moderate canopy cover regimes but reveal a systematic underestimation at cover levels exceeding ~90%. For urban Würzburg scenarios — where total canopy coverage rarely exceeds 40–60% even in the most heavily treed areas — this limitation is unlikely to be binding.

## Key Claims

1. The Crookston & Stage random overlap model performs best only in the driest, least productive forest type (wmdrycon); for mesic and wet forest types it underestimates line-intercept cover at high density.
2. Adjusted crown-width methods (social position adjustment + subplot cap at 120%) achieve RMSE ≈ 12–14% cover across all forest types — a practical, transferable approach.
3. The mean empirical overlap correction factor across all plots is **OCF_e = 0.015**, slightly above the Crookston & Stage default of 0.01 — crowns overlap slightly more dispersedly (less randomly) than the Poisson assumption implies in productive stands.
4. Statistical models using stand structure variables (dominant tree height + December minimum temperature + site productivity) achieve RMSE ≈ 11.9% — marginally better but region-specific.
5. Simple summing of raw crown areas (no overlap correction) consistently overestimates canopy cover even at low density levels.

## Data and Figures

| Method | RMSE (% cover, all plots) |
|---|---|
| Raw crown area sum (no overlap) | >> 14 |
| Random overlap, Crookston & Stage 1999 (New_olap) | 14.0 |
| Height-adjusted + subplot cap (New_ht_cap) | ~12.5 |
| Crown class-adjusted + subplot cap (Old_crn_cap) | ~12.0 |
| Predicted overlap correction factor model | 12.5 |
| Maximum likelihood statistical model | 11.9 |

## Contradictions / Gaps

- Study area is US Pacific Northwest forests — species and density regimes differ from Central European urban trees. The social-position adjustments (overstory/suppressed classification) do not translate directly to single-tree urban inventory data where trees are typically open-grown.
- The finding that OCF_e = 0.015 > 0.01 (i.e., crowns are slightly more dispersed than random) is consistent with urban trees being deliberately spaced — if anything, the Crookston & Stage formula with its default 0.01 exponent may *over-predict* overlap for well-spaced urban planting scenarios, meaning the simulation may slightly *underestimate* effective new canopy coverage.
- All RMSEs are dominated by sampling error in the study design (comparing two independent samples from the same stand), not model error — real model error is likely lower.

## Wiki Pages Updated

- [[wiki/simulation-logic]] — Beer-Lambert overlap model validated; OCF caveat documented; high-density limitation noted
- [[wiki/concepts/green-infrastructure]] — canopy cover estimation methodology reference
