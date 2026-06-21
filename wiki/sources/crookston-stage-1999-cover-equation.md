---
title: "Crookston & Stage 1999 — Negative Exponential Cover Equation"
type: source
tags: [canopy-cover, overlap-model, simulation, forest, urban-trees]
sources: 1
updated: 2026-06-21
---

# Source: Crookston & Stage 1999 — Negative Exponential Cover Equation

- **Type:** technical report
- **Author(s):** Nicholas L. Crookston, Andrew R. Stage
- **Date:** 1999
- **Publisher:** USDA Forest Service, Rocky Mountain Research Station
- **Report:** General Technical Report RMRS-GTR-24
- **Raw file:** (kein raw-Clip vorhanden — Herleitung aus Implementierungskontext)

## Summary

Crookston & Stage (1999) leiten die negativ-exponentielle Gleichung zur Schätzung der
projizierten Kronendeckung (canopy cover) aus einzelnen Kronenflächen-Summen her. Die
Gleichung nimmt eine zufällige (Poisson-)Verteilung der Kronenüberlappungen an und liefert
dadurch eine Schätzung der *Vereinigungsfläche* aller Kronen — im Gegensatz zur naiven
Summe, die bei dichten Beständen die tatsächliche Bodenabdeckung systematisch überschätzt.

Die zentrale Gleichung lautet:

```
CC = (1 − exp(−Σ Kronenfläche / Bezugsfläche)) × 100
```

Wobei `CC` die projizierte Kronendeckung in Prozent ist. Der Ausdruck
`Σ Kronenfläche / Bezugsfläche` wird als Flächen-Verhältnis (ratio) bezeichnet. Das Modell
ist asymptotisch: auch bei unendlich vielen Bäumen bleibt `CC < 100 %`.

## Key Claims

1. Die naive Summe `Σ Kronenfläche / Bezugsfläche × 100 %` überschätzt die projizierte
   Bodenabdeckung in dichten Beständen erheblich, da reale Kronen sich überlappen.
2. Die negativ-exponentielle Gleichung (Beer-Lambert-Analogie) korrigiert diesen Fehler
   unter der Annahme zufälliger Kronenplatzierung.
3. Die Inversformel lautet: `ratio = −ln(1 − CC/100)`, was die Addition von Bestand und
   Neupflanzungen im selben Projektionsraum erlaubt (kein Mischen von projizierten
   Prozentwerten und Kronenflächen-Verhältnissen).
4. Bei regelmäßig gepflanzten Alleen (z. B. Straßenbäume) unterschätzt das Modell leicht;
   bei unregelmäßigen Park-Clustern überschätzt es leicht.

## Data and Figures

- Für ein Flächen-Verhältnis von 0,5 (z. B. 5.000 m² Kronenfläche auf 10.000 m²) ergibt
  sich: `(1 − exp(−0,5)) × 100 ≈ 39,3 %` (statt naiv 50,0 %).
- Für ratio = 1,0: `(1 − exp(−1)) × 100 ≈ 63,2 %` (statt naiv 100 %).
- Für ratio = 5,0: `(1 − exp(−5)) × 100 ≈ 99,3 %` (asymptotisch).

## Einsatz in Resilientes Würzburg

Die Gleichung wird in zwei Kontexten genutzt:

1. **`_compute_bestand_pct` (data_loader.py):** Berechnet die projizierte Kronendeckung
   je 100-m-Rasterzelle aus dem Baumkataster (Σ `π×(kronenbrei/2)²` per Zelle).
2. **`simulate_baeume` (routers/simulate.py):** Addiert Bestand und Neupflanzungen im
   Projektionsraum, um den realen Deckungszuwachs `effective_new_pct` zu berechnen.

Implementierung in `simulation_params.py`:
- `projected_cover_pct(ratio)` — Vorwärtsformel
- `inverse_ratio(pct)` — Inversformel (log-sicher, klemmt bei 99,9 %)

## Contradictions / Gaps

- Annahme zufälliger Kronenüberlappung ist vereinfachend. Bei systematischer Reihenpflanzung
  (Alleen) leichte Unterschätzung; bei geklumpten Beständen leichte Überschätzung.
  Empirische Validierung für städtische Umgebungen: [[wiki/sources/gray-2021-canopy-cover-prediction]].
- Modell liefert *projizierte Deckung*, keine Lichtdurchlässigkeit (Canopy Closure ≠ Cover).
  Distinction nach Jennings et al. (1999, *Forestry* 72(1)) relevant für Transpirationsmodelle.

## Wiki Pages Updated

- [[wiki/simulation-logic]] — Inputs/Outputs, Schritt 1, Quellverweis ergänzt
- [[wiki/concepts/entsiegelung]] — (kein Bezug zu Entsiegelung)
