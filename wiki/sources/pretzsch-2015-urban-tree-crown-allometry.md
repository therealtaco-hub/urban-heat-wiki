---
title: "Source: Pretzsch et al. 2015 — Crown Size Allometry for 22 Urban Tree Species"
type: source
tags: [trees, allometry, crown-radius, crown-size, urban-forestry, worldwide, species-classification]
sources: 1
updated: 2026-06-19
---

# Source: Crown Size and Growing Space Requirement of Common Tree Species in Urban Centres, Parks, and Forests

- **Type:** journal article
- **Author(s):** Hans Pretzsch, Peter Biber, Enno Uhl, Jens Dahlhausen, Thomas Rötzer et al.
- **Date:** 2015
- **Journal:** Urban Forestry & Urban Greening 14(3):466–479
- **DOI:** http://dx.doi.org/10.1016/j.ufug.2015.04.006
- **Raw file:** [[raw/2015 Pretzsch et al Urban tree crowns UFUG 14(3)466-479.pdf]]

## Summary

Pretzsch et al. derived species-specific crown radius–stem diameter allometries for 22 common urban tree species worldwide, using 39,057 single-tree observations from nine cities (Munich, Paris, Sapporo, Brisbane, Hanoi, Prince George CA, Santiago de Chile, Cape Town, Berlin) and Southern German long-term forest research plots. The allometric model is `ln(cr) = a + α × ln(d)` (equivalent to `cr = e^a × d^α`), fitted at the 95th percentile quantile to represent open-grown conditions typical of urban trees.

By k-means cluster analysis on two parameters — cr25 (crown radius at DBH = 25 cm) and the allometric exponent α — the 22 species were grouped into **5 allometric types**. The four species most common in the Würzburg Baumkataster (*Tilia cordata*, *Platanus × hispanica*, *Aesculus hippocastanum*, *Robinia pseudoacacia*) all fall into **Allometric Type 1 "Large Crown Size – Moderate Allometric Slope"**, which has the largest absolute crown dimensions of all five types.

This paper is the **widest-coverage allometric reference** for urban trees and the foundational source for the more Würzburg-specific study by [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]].

## Key Claims

1. All four species dominant in Würzburg's Baumkataster belong to Allometric Type 1 — the largest-crowned type.
2. Mean crown projection area for Type 1 at DBH = 25 cm: **65.6 m²** (mean crown radius 4.6 m, CPA = π × cr²).
3. Species-specific crown radius at DBH = 25 cm (95th percentile, open-grown): Tilia cordata 4.5 m, Platanus × hispanica 4.7 m, Aesculus hippocastanum 4.0 m, Robinia pseudoacacia 4.2 m.
4. Allometric exponent α for crown radius: Type 1 mean ≈ 0.58 — a 1% increase in DBH leads to a 0.58% increase in crown radius.
5. Tree height allometry is shallower than crown radius allometry and less competition-sensitive; crown width is the primary driver of growing-space requirement.
6. Crown volume allometry converges across types (most species: α_cv ≈ 2 × α_cr + α_h), confirming theoretical allometry.

## Data and Figures

Species-specific allometric coefficients for `ln(cr) = a + α × ln(d)` (95th quantile, open-grown):

| Species | n | a | α | cr25 (m) | CPA at 25 cm (m²) |
|---|---|---|---|---|---|
| *Tilia cordata* | 353 | −0.338 | 0.573 | 4.5 | 63.6 |
| *Platanus × hispanica* | 171 | −0.554 | 0.653 | 4.7 | 69.4 |
| *Aesculus hippocastanum* | 230 | −0.548 | 0.601 | 4.0 | 50.3 |
| *Robinia pseudoacacia* | 135 | −0.435 | 0.582 | 4.2 | 55.4 |

Allometric Type 1 mean parameters (usable for species not in table): a = −0.351, α = 0.581, cr25 = 4.6 m, cpa25 = 65.6 m²

Application for any individual tree: `cr_m = exp(a) × DBH_cm^α`, then `CPA_m2 = π × cr_m²`

## Contradictions / Gaps

- The 95th-percentile regression represents open-grown (maximally crowned) trees; average urban trees with any spatial competition will have smaller crowns. For a population average, the 50th-percentile coefficients (also available in the source) are more appropriate. Moser-Reischl 2021 uses ordinary least squares (OLS) at the mean — their results for Würzburg trees should therefore be preferred over Pretzsch 2015 95th-percentile for population-average calculations.
- The Type 1 mean CPA at DBH=25 cm (65.6 m²) is substantially higher than our simulation default of 50 m² — this default is conservative for mature trees but may overestimate for young trees (DBH < 15 cm where CPA is ~15–25 m²).
- Worldwide dataset mixes trees from very different climates; for Würzburg, the South German and Munich data points within this dataset are most relevant.

## Wiki Pages Updated

- [[wiki/concepts/tree-species-selection]] — allometric type classification; species-specific cr25 and CPA values
- [[wiki/simulation-logic]] — crown area default caveat; allometric formula documented as improvement path
- [[wiki/entities/thomas-roetzer]] — co-author (Rötzer listed)
- [[wiki/entities/tu-muenchen]] — institutional home of Pretzsch + Rötzer
- [[wiki/kuehleffekte-vergleich]] — CPA reference values for Type 1 species
