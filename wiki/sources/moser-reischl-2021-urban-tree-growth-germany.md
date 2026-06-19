---
title: "Source: Moser-Reischl et al. 2021 — Urban Tree Growth in South Germany"
type: source
tags: [trees, allometry, crown-size, south-germany, würzburg, urban-forestry, growth-model]
sources: 1
updated: 2026-06-19
---

# Source: Urban Tree Growth Characteristics of Four Common Species in South Germany

- **Type:** journal article
- **Author(s):** Astrid Moser-Reischl, Thomas Rötzer, Stephan Pauleit, Hans Pretzsch
- **Date:** 2021
- **Journal:** Arboriculture & Urban Forestry 47(4):150–169
- **DOI:** https://doi.org/10.48044/jauf.2021.015
- **Raw file:** [[raw/Moser-Reischl et al. (2021), Arboric. & Urban For. 47(4).pdf]]

## Summary

Moser-Reischl et al. developed allometric relationships for four common urban tree species in South Germany: horse chestnut (*Aesculus hippocastanum*), small-leaved lime (*Tilia cordata*), black locust (*Robinia pseudoacacia*), and plane tree (*Platanus × hispanica*). The study measured 2,003 trees across six cities from 2014–2017: Munich, **Würzburg**, Nuremberg, Bayreuth, Hof, and Kempten. Among the six cities, Würzburg is characterized as the warmest (avg. 9.6 °C/yr, tied with Munich) and driest (599 mm/yr precipitation) — conditions directly relevant to how Würzburg's urban trees develop.

Allometric regressions were fitted for tree height (TH), crown projection area (CPA), crown diameter (CD), crown length (CL), crown volume (CV), and leaf area index (LAI) against diameter at breast height (DBH), using log-transformation. The paper enables calculation of species-specific crown projection areas from DBH alone, which — combined with the Würzburg Baumkataster field `kronenbrei` (crown diameter measured in the field) — provides a direct route to computing `kronenfläche_m2` for all 44,647 trees.

Growth differences between sites (park, street, square) were marked: park trees consistently had the largest DBH, height, and crown dimensions. Site type is therefore an important correction factor when modeling ecosystem services from the Baumkataster, since a park *Tilia* will cool considerably more than a street *Tilia* of the same age.

## Key Claims

1. Crown projection area (CPA) of *Platanus × hispanica* is the largest of the four species on average: 113.7 m² across all six cities (this reflects mature trees across all age classes).
2. For *Tilia cordata* in Würzburg specifically: mean DBH 30.5 cm, mean CPA 62.1 m², mean age 41 years (n=86).
3. *Robinia pseudoacacia*: fastest initial growth but structural development slows markedly at DBH ≈ 20 cm.
4. *Aesculus hippocastanum*: oldest on average (68 years), slowest height increment.
5. Differences between cities are minor for trees younger than 100 years; within-city site variation (park vs. street) is the dominant growth driver.
6. Park trees have the greatest tree structures for all species (P < 0.001 vs. street and square).
7. Obstacles (buildings, other trees) south of the tree have a measurable negative influence on crown growth in all species.

## Data and Figures

Species-specific log-linear allometric coefficients for `ln(CPA) = a + b × ln(DBH)` — all South German cities pooled:

| Species | a | b | R² |
|---|---|---|---|
| *A. hippocastanum* | −0.477 | 1.230 | 0.79 |
| *P. × hispanica* | −0.825 | 1.505 | 0.84 |
| *R. pseudoacacia* | −0.164 | 1.181 | 0.71 |
| *T. cordata* | −1.081 | 1.448 | 0.86 |

Application: `CPA_m2 = exp(a) × DBH_cm^b`

Würzburg-specific mean values (Table 2, from study):

| Species | n | Age (yr) | DBH (cm) | Height (m) | CPA (m²) |
|---|---|---|---|---|---|
| *A. hippocastanum* | 75 | 53.7 | 38.6 | 13.0 | 69.0 |
| *P. × hispanica* | 79 | 33.1 | 37.3 | 15.7 | 124.1 |
| *R. pseudoacacia* | 89 | 43.9 | 44.1 | 15.4 | 86.3 |
| *T. cordata* | 86 | 41.0 | 30.5 | 12.2 | 62.1 |

## Contradictions / Gaps

- The Baumkataster field `kronenbrei` is the measured crown diameter — this gives CPA directly via `CPA = π × (kronenbrei/2)²` without needing the allometric regression. The regression is the fallback when `kronenbrei` is null or zero.
- Species coverage limited to 4 of the most common Central European urban tree species; for the remaining Baumkataster species → [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]] covers 22 species globally.
- Growth functions derived from 2014–2017 measurements; accelerating warming trends may alter future growth trajectories, particularly for drought-sensitive species in Würzburg.

## Wiki Pages Updated

- [[wiki/concepts/tree-species-selection]] — species-specific CPA data for Würzburg; park/street site-type effect
- [[wiki/simulation-logic]] — kronenfläche calculation route; allometric alternative to fixed 50 m² default
- [[wiki/entities/thomas-roetzer]] — co-author
- [[wiki/entities/wuerzburg]] — Würzburg is a direct study city with n=75–89 per species
- [[wiki/entities/tu-muenchen]] — institutional home (Rötzer, Pauleit, Pretzsch at TU München)
- [[wiki/overview]] — allometric data closes the kronenfläche TODO
