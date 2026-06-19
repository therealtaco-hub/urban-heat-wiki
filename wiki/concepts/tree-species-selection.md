---
title: "Tree Species Selection and the Drought-Cooling Tradeoff"
type: concept
tags: [trees, drought-tolerance, transpiration, species-selection, climate-adaptation, tradeoff, allometry, crown-size]
sources: 3
updated: 2026-06-19
---

# Tree Species Selection and the Drought-Cooling Tradeoff

The tension between selecting climate-resilient (drought-tolerant) tree species for long-term survival under climate change, and selecting high-performing cooling species for maximum evapotranspirative and shading benefit. Drought-tolerant species transpire less — which is what makes them drought-tolerant — but this directly reduces their cooling contribution. A parallel design dimension is **crown size**: larger-crowned species deliver more shading and more crown-area-based cooling, independent of drought tolerance.

## Key Facts

### Transpiration (drought–cooling tradeoff)
- Drought-tolerant street trees (LB6: *Acer campestre*, *Ostrya carpinifolia*, *Tilia tomentosa* 'Brabant') transpire **0.17 kg H₂O m⁻² day⁻¹** on average — 11% less than moisture-adapted species.
- Moisture-adapted trees (LB3: *Acer platanoides*, *Carpinus betulus* 'Fastigiata', *Tilia cordata* 'Greenspire') transpire **0.19 kg H₂O m⁻² day⁻¹**. *(Source: [[wiki/sources/klimabaeume-fuer-die-stadt]])*
- The tradeoff is real but **modest under sufficient soil moisture** — the divergence likely grows under drought conditions.
- LB6 trees show higher water use efficiency (1.12× higher max xylem flux density, up to 7× higher growth per unit water used).
- Both shade and transpiration — the two cooling mechanisms — correlate with biomass production and water use, which are both reduced in drought-adapted species.

### Crown size and allometric type (for Würzburg species)

All four species most common in the Würzburg Baumkataster belong to **Allometric Type 1 "Large Crown Size – Moderate Slope"** *(Pretzsch et al. 2015)* — the largest-crowned class of the 22 studied species. *(Source: [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]])*

| Species | cr at DBH=25 cm | CPA at DBH=25 cm | Note |
|---|---|---|---|
| *Tilia cordata* | 4.5 m | ~64 m² | High LAI; native |
| *Platanus × hispanica* | 4.7 m | ~69 m² | Fastest height growth |
| *Aesculus hippocastanum* | 4.0 m | ~50 m² | Oldest; slowest height increment |
| *Robinia pseudoacacia* | 4.2 m | ~55 m² | Fast early growth; slows at DBH ~20 cm |

Values represent open-grown 95th percentile. For population-average CPA from Würzburg measurements see [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]].

Würzburg-specific mean CPA by species (from 2014–2017 field measurements in Würzburg, all site types):

| Species | n (Würzburg) | Mean DBH | Mean CPA |
|---|---|---|---|
| *A. hippocastanum* | 75 | 38.6 cm | 69.0 m² |
| *P. × hispanica* | 79 | 37.3 cm | 124.1 m² |
| *R. pseudoacacia* | 89 | 44.1 cm | 86.3 m² |
| *T. cordata* | 86 | 30.5 cm | 62.1 m² |

### Site type effect on crown size
Park trees have significantly larger crowns, height, and DBH than street or square trees across all four Würzburg species. This means a park *Tilia* cools materially more than a street *Tilia* of the same age — site type must be accounted for in any per-tree ecosystem service estimate. *(Source: [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]])*

## Implications for Planning

- Planting drought-tolerant trees to ensure survival under climate change will likely deliver **less cooling per tree** than moisture-adapted species.
- This tradeoff must be explicitly reflected in urban greening strategies and cooling simulations — a tree planted today under a climate-resilient species choice may cool 10–15% less than one planted with a moisture-adapted species.
- The tradeoff may be acceptable given longer expected survival: a drought-tolerant tree that lives 40 years cools more over its lifetime than a moisture-adapted tree that dies in 20 years due to drought stress.
- Among the Würzburg Baumkataster species, *Platanus × hispanica* delivers the largest crown projection area per tree but has a low LAI; *Tilia cordata* has the highest LAI (best transpiration cooling) and is native.
- Computing `kronenfläche_m2 = π × (kronenbrei/2)²` from the existing `kronenbrei` field in the Baumkataster is now justified by allometric data — and can be enhanced with the allometric regression `CPA = exp(a) × DBH^b` when `kronenbrei` is null.

## Related Concepts

- [[wiki/concepts/evapotranspiration]] — the mechanism affected
- [[wiki/concepts/green-infrastructure]] — where species choice matters
- [[wiki/concepts/urban-heat-island]] — the outcome being mitigated

## Relevant Entities

- [[wiki/entities/thomas-roetzer]] — committee chair for the Klimabäume dissertation; co-author on Moser-Reischl 2021 and Pretzsch 2015
- [[wiki/entities/tu-muenchen]] — research institution
- [[wiki/entities/wuerzburg]] — target city; Würzburg data included in Moser-Reischl 2021

## Sources

- [[wiki/sources/klimabaeume-fuer-die-stadt]] — drought–cooling tradeoff; LB3/LB6 transpiration rates
- [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]] — Würzburg-specific allometric tables; site-type effect
- [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]] — worldwide allometric type classification; cr25 values
