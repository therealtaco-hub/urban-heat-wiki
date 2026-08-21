---
title: "Source: Chen et al. 2018 — Spatially Explicit Heat Health Risk, Yangtze River Delta"
type: source
tags: [vulnerability, hvi, lst, grid-based, pca, crichton-risk-triangle, china]
sources: 1
updated: 2026-08-18
---

# Source: Spatially explicit assessment of heat health risk by using multisensor remote sensing images and socioeconomic data in Yangtze River Delta, China

- **Type:** paper
- **Author(s):** Qian Chen, Mingjun Ding, Xuchao Yang, Kejia Hu, Jiaguo Qi
- **Date:** 2018
- **Venue:** *International Journal of Health Geographics* 17:15, DOI 10.1186/s12942-018-0135-y
- **Raw file:** not in wiki `raw/` — held as `resilientes_wuerzburg/paper/12942_2018_Article_135.pdf` in the code project

## Summary
This paper builds a pixel-level (250m resolution) composite heat-health-risk index for the Yangtze River Delta megaregion (China, ~112,600 km², including Shanghai, Hangzhou, Nanjing and 13 other cities), following Crichton's Risk Triangle framework: Risk = Hazard × Exposure × Vulnerability, all three components computed as independent gridded layers and combined by equal-weighted multiplication. Heat hazard comes from two clear-sky MODIS LST images (daytime + nighttime) during an August 2013 heatwave. Human exposure is estimated not from raw census population but from an "elevation-adjusted human settlement index" (EAHSI) combining nighttime-lights imagery, vegetation index, and a DEM-based elevation correction — validated against county-level census population (R²=0.87) as a way to disaggregate population below the administrative-unit level. Heat vulnerability is a PCA-derived index from six county-level socioeconomic variables (age 65+, elderly living alone, illiteracy, per-capita GDP, hospital beds, air-conditioning ownership).

The key finding is that high-risk areas are not simply "the hottest places" — they are driven by the *interaction* of hazard, exposure, and vulnerability, and can occur in less-urbanized areas with only moderate heat if vulnerability is high (low income/education, high elderly-living-alone rate), while some very hot central-city areas have low risk because high socioeconomic status offsets the heat hazard.

## Key Claims
1. Grid/pixel-based composite risk assessment (not administrative-unit-based) is achievable at fine spatial resolution (250m here) by combining independently-sourced remote sensing (LST, nighttime lights, vegetation) with census-based vulnerability — directly analogous in spirit to this project's 100m-grid LST↔Zensus join, though this paper interpolates/disaggregates population from county-level census rather than using a native fine grid.
2. PCA on six vulnerability variables reduced to two principal components explaining ~65% of variance: "socioeconomic status" (48.24%, dominated by air-conditioning ownership, GDP, hospital beds, illiteracy — inverted) and "age" (17.12%, driven by % population 65+).
3. Multiplicative (hazard × exposure × vulnerability) risk combination, rather than additive/weighted-sum — a direct methodological contrast to this project's additive weighted HVI (0.6×LST + 0.4×elderly).
4. High social vulnerability can dominate risk outcomes even where heat hazard is only moderate — risk maps show some rural/suburban areas at higher composite risk than hotter urban cores, because urban cores have offsetting high socioeconomic status.
5. No standard weighting scheme exists in the literature for combining hazard/exposure/vulnerability layers — this paper, like several others reviewed, defaults to equal weighting for lack of an evidence-based alternative.
6. Nighttime LST is highlighted as an important and often-omitted hazard component (most heat-risk studies use daytime LST only), since nocturnal urban heat island intensity drives much of heat-related mortality risk via lack of overnight relief.

## Data and Figures
- Study area: 112,642 km², 16 cities, subtropical monsoon climate, 250m pixel resolution.
- Daytime LST during heatwave: 27–48°C; nighttime LST spatial gradient weaker but still shows clear UHI signature (~30°C+ in urban cores).
- EAHSI vs. county population correlation: R²=0.87.
- PCA vulnerability: component 1 (socioeconomic) 48.24% variance, component 2 (age) 17.12% variance.

## Contradictions / Gaps
- Uses multiplicative hazard×exposure×vulnerability combination — worth citing as an alternative risk-composition philosophy against this project's additive weighted-sum HVI (no exposure/population term is separately multiplied in; population weighting only enters via the district-level population-weighted HVI aggregate in `/api/stadtbezirke`).
- No small-numbers/shrinkage correction for county-level vulnerability variables — same gap as the other Cluster 2 sources.
- County-level administrative units for vulnerability (not truly pixel-native) — the EAHSI exposure layer is the only genuinely fine-grained component; vulnerability itself is spatially smoothed within county boundaries, a limitation the paper's own discussion acknowledges.

## Wiki Pages Updated
- [[wiki/overview]]
- [[wiki/concepts/heat-vulnerability-index]] (new)
- [[wiki/index]]
