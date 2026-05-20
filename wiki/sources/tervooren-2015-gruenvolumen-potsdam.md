---
title: "Source: Potenziale von Grünvolumen und Entsiegelung zur Klimaanpassung am Beispiel der Landeshauptstadt Potsdam"
type: source
tags: [entsiegelung, grünvolumen, landsat, potsdam, regression, temperatur, schlüsselquelle]
sources: 1
updated: 2026-05-20
---

# Source: Tervooren (2015) — Grünvolumen und Entsiegelung in Potsdam

- **Type:** Konferenzbeitrag (AGIT — Journal für Angewandte Geoinformatik, 2015)
- **Autor:** Steffen Tervooren (Landeshauptstadt Potsdam / UNIGIS Salzburg)
- **DOI:** 10.14627/537557037
- **Klima Potsdam:** Cfb (gemäßigt-ozeanisch) — vergleichbar mit Würzburg
- **Raw file:** [[raw/537557037.pdf]]

## Summary

Diese Studie korreliert Landsat-LST-Daten (2010, heißer Sommertag, DWD-Lufttemperatur bis ~39°C) mit Grünvolumen (GV) und Versiegelungsgrad (VG) für Potsdam. Auf Basis von Biotop-Polygondaten und linearer sowie geographisch gewichteter Regression (GWR) werden quantitative Formeln für den Zusammenhang zwischen Versiegelung und LST abgeleitet. Die Studie bestätigt und erweitert die Manchester-Ergebnisse (Gill 2006/2007) für einen deutschen Stadtkontext.

**Das Kernergebnis**: Jede 1% zusätzliche Versiegelung geht mit einem Temperaturanstieg von 0,03°C einher — bzw. umgekehrt: jede 1% Entsiegelung senkt die LST um 0,03°C. Diese Formel ist der bisher einzige im Wiki vorhandene Entsiegelungskoeffizient in °C/% und füllt die zentrale Lücke im methodischen Plan.

## Key Claims

1. **ΔTempVG = 0,03 × ΔVG [%]** — Formel für Temperaturänderung durch Versiegelungsänderung. 1% Entsiegelung → −0,03°C LST. *(Modellgüte: R²=0,75 OLR, R²=0,80 GWR)*
2. Grünvolumen korreliert negativ mit Temperatur: **R²=0,905 (linear), R²=0,957 (quadratisch)** — sehr hohe Modellgüte.
3. Manchester-Replikation bestätigt: 10% Steigerung des Grünvolumens → **−2,2 bis −2,5°C** Temperaturreduktion (Gill 2006/2007, orig. für Manchester).
4. GV und VG sind stark kreuzkorreliert — sie beeinflussen sich gegenseitig, wirken nicht unabhängig additiv.
5. Referenzwerte für einen heißen Sommertag in Potsdam (9. Juli 2010): DWD Lufttemperatur 37,3°C; Bodenoberfläche 31,9°C; Landsat-Oberflächentemperatur 30,1°C; Polygon-Durchschnitt 29,0°C.
6. Potsdam-Klimazone: Cfb — nächste Vergleichszone zu Würzburg (Dfb) im Wiki.

## Daten und Formeln

| Formel | Interpretation |
|--------|---------------|
| ΔTempVG = 0,03 × ΔVG [%] | 1% mehr Versiegelung → +0,03°C LST; 1% Entsiegelung → −0,03°C LST |
| 10% GV-Steigerung → −2,2 bis −2,5°C | Manchester-Referenz, in Potsdam bestätigt |

**Vergleich mit Baumkorrelation:**
- Entsiegelung: −0,03°C pro 1% Flächenentiegelung
- Baumpflanzung: −0,069°C pro 1% Baumkronendeckung *(García de León et al.)*
- → Bäume kühlen rein temperaturmäßig ~2,3× stärker pro Prozentpunkt als reine Entsiegelung
- → Aber: Entsiegelung hat Zusatzeffekte (Infiltration, Grundwasser, Artenvielfalt) die Bäume allein nicht liefern

## Contradictions / Gaps

- Eintags-Analyse (ein heißer Sommertag 2010) — saisonale Verallgemeinerbarkeit nicht geprüft.
- Formel für Potsdam/Cfb — Übertragung auf Würzburg/Dfb plausibel aber nicht direkt validiert.
- GV und VG sind kreuzkorreliert; Isolierung der Entsiegelungswirkung von der Bepflanzungswirkung methodisch schwierig.

## Wiki Pages Updated

- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] ← this page
- [[wiki/concepts/entsiegelung]]
- [[wiki/concepts/impervious-surface]]
- [[wiki/concepts/land-surface-temperature]]
- [[wiki/kuehleffekte-vergleich]]
- [[wiki/methodischer-plan-wuerzburg]]
- [[wiki/overview]]
