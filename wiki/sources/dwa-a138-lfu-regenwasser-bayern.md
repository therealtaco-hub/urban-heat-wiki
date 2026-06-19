---
title: "DWA-A138 Anwendung bei der Regenwasserbewirtschaftung in Bayern (LfU)"
type: source
tags: [entsiegelung, versickerung, abflussbeiwert, regenwasser, lfu-bayern, dwa-a138, hydrologie]
sources: 1
updated: 2026-06-08
---

# Source: DWA-A138 — Regenwasserbewirtschaftung Bayern (LfU)

- **Type:** Fachpräsentation / Behördenleitfaden
- **Author(s):** Florian Ettinger, Bayerisches Landesamt für Umwelt (LfU), Referat 67
- **Date:** undatiert (Bezug auf DWA-A138-Standard; Präsentation nach 2020)
- **Raw file:** [[raw/dwa_a138_lfu.pdf]]

## Summary

Das Bayerische Landesamt für Umwelt (LfU) präsentiert die Anwendung des deutschen Regelwerks DWA-A138 (*Planung, Bau und Betrieb von Anlagen zur Versickerung von Niederschlagswasser*) für die Praxis in Bayern. Das DWA-A138 ist das in Deutschland verbindliche technische Regelwerk für dezentrale und zentrale Regenwasserversickerung.

Das Dokument deckt drei Themenbereiche ab: (1) **Abflussbeiwerte** nach Belagstyp als Bemessungsgrundlage — dies ist die behördlich anerkannte Bayerische Tabelle und damit die Quelle für die in `simulation_params.py` verwendeten Werte; (2) **Untergrundparameter** (Durchlässigkeitsbeiwerte kf, Grundwasserabstand) als Standortbedingungen für Versickerungsanlagen; (3) **Anlagentypen** (Mulden, Rigolen, Sickerschächte) und deren Bemessungsverfahren.

Für das Projekt *Resilientes Würzburg* ist dies die **maßgebliche Quelle für die Abflussbeiwerte**, die im `/api/simulate/wasser`-Endpoint die Versickerungsberechnung steuern. Die Werte sind direkt für Bayern (inkl. Würzburg) gültig. Die Leitfaden-Bayreuth-2024-Quelle, die bislang als Quellenbeleg diente, zitiert ihrerseits das DWA-A138 als Ursprung.

## Key Claims

1. **Asphalt / fugenloser Beton: Ψ = 0,9** — maßgeblicher DWA-A138-Wert für vollversiegelte Fahrbahnen/Plätze. (Hinweis: `simulation_params.py` verwendet aktuell 0,95 aus Leitfaden Bayreuth — kleiner Unterschied; DWA-A138 ist die primäre Quelle.)
2. **Pflaster mit dichten Fugen: Ψ = 0,75** — relevanter Zwischenbelag für Plätze und ältere Straßen.
3. **Fester Kiesbelag: Ψ = 0,60** — mittlere Durchlässigkeit.
4. **Pflaster mit offenen Fugen: Ψ = 0,50** — entspricht dem in `simulation_params.py` als `sickerpflaster` geführten Wert (0,30 stammt aus Leitfaden Bayreuth als Mittelwert einer breiten Bandbreite).
5. **Verbundsteine mit Fugen / Sickersteine: Ψ = 0,25** — teilversiegelt.
6. **Rasengittersteine: Ψ = 0,15** — übereinstimmend mit `simulation_params.py` (`rasengitter: 0.15`).
7. **Lockerer Kiesbelag / Schotterrasen: Ψ = 0,30** — übereinstimmend mit `simulation_params.py` (`schotterrasen: 0.30`).
8. **Gärten, Wiesen, Kulturland (flach): Ψ = 0,0–0,1** — bestätigt den `rasendecke: 0.05`-Wert.
9. **Gründach (humusiert > 10 cm): Ψ = 0,30; < 10 cm: Ψ = 0,50; Kiesauflage: Ψ = 0,70** — für zukünftige Dachbegrünungs-Simulation relevant (derzeit nicht in `simulation_params.py`).
10. **Schrägdach**: Ziegel/Dachpappe Ψ = 0,8–1,0; Metall/Glas/Schiefer Ψ = 0,9–1,0.
11. **Versickerungseignung**: Bester kf-Bereich 10⁻⁴ bis 10⁻³ m/s (sandiger Kies, Grob-/Mittelsand). Toniger Schluff/Ton (< 10⁻⁷ m/s) nicht versickerungsfähig.
12. **Mindestabstand Grundwasser**: ≥ 1 m zum mittleren Höchsten Grundwasserstand (MHGW). Ausnahme bei geringer Belastung und ≥ 20 cm bewachsenem Oberboden: Abstand nur zum MGW.
13. **Vorbehandlung**: Zwei Ziele — Schadstoffrückhalt (Grundwasserschutz, DWA-M 153 / TRENGW Bayern) und Rückhalt von Feinpartikeln (Kolmationsschutz). Verfahren abhängig von Belagsklasse (Dach/Kfz-Fläche/Sonderfläche).
14. **Regendaten Bayern**: DWD-KOSTRA-Statistik (±10–20% Toleranz); für Langzeitsimulation: NiedSimBY (synthetische Niederschlagsreihen Bayern).
15. **Vereinfachtes Bemessungsverfahren** (analog DWA-A117): anwendbar bei AE ≤ 200 ha, Fließzeit ≤ 15 min, spezifischer Versickerungsrate qs ≥ 2 l/(s·ha).

## Data and Figures

**Vollständige Abflussbeiwert-Tabelle (DWA-A138 / LfU Bayern):**

| Flächentyp | Belagsart | Ψ (Abflussbeiwert) |
|---|---|---|
| Schrägdach | Metall, Glas, Schiefer, Faserzement | 0,9–1,0 |
| Schrägdach | Ziegel, Dachpappe | 0,8–1,0 |
| Flachdach (≤ 3°) | Metall, Glas, Faserzement | 0,9–1,0 |
| Flachdach (≤ 3°) | Dachpappe | 0,9 |
| Flachdach (≤ 3°) | Kiesauflage | 0,7 |
| Gründach (≤ 15°) | humusiert < 10 cm | 0,5 |
| Gründach (≤ 15°) | humusiert > 10 cm | 0,3 |
| Straßen, Wege, Plätze | Asphalt, fugenloser Beton | 0,9 |
| Straßen, Wege, Plätze | Pflaster mit dichten Fugen | 0,75 |
| Straßen, Wege, Plätze | Fester Kiesbelag | 0,6 |
| Straßen, Wege, Plätze | Pflaster mit offenen Fugen | 0,5 |
| Straßen, Wege, Plätze | Lockerer Kiesbelag, Schotterrasen | 0,3 |
| Straßen, Wege, Plätze | Verbundsteine mit Fugen, Sickersteine | 0,25 |
| Straßen, Wege, Plätze | Rasengittersteine | 0,15 |
| Böschungen, Bankette | Toniger Boden | 0,5 |
| Böschungen, Bankette | Lehmiger Sandboden | 0,4 |
| Böschungen, Bankette | Kies- und Sandboden | 0,3 |
| Gärten, Wiesen, Kulturland | Flaches Gelände | 0,0–0,1 |
| Gärten, Wiesen, Kulturland | Steiles Gelände | 0,1–0,3 |

**Bodendurchlässigkeit (kf-Werte):**

| Bodenart | kf-Bereich | Versickerungseignung |
|---|---|---|
| Grobkies | > 10⁻² m/s | zu schnell (Filterprobleme) |
| Sandiger Kies, Grobsand | 10⁻³–10⁻² m/s | gut |
| Mittelsand | 10⁻⁴–10⁻³ m/s | gut (optimaler Bereich) |
| Feinsand | 10⁻⁵–10⁻⁴ m/s | eingeschränkt |
| Schluffiger Sand | 10⁻⁶–10⁻⁵ m/s | kaum geeignet |
| Ton, schluffiger Ton | < 10⁻⁷ m/s | nicht geeignet |

## Contradictions / Gaps

- **Asphalt-Wert**: DWA-A138 gibt 0,9; `simulation_params.py` verwendet 0,95 (aus Leitfaden Bayreuth 2024). Die Differenz ist gering, aber DWA-A138 ist die primäre Normenquelle — Anpassung in `simulation_params.py` auf 0,90 wäre korrekt (oder als Bandbreite 0,9–1,0 dokumentieren).
- **Sickerpflaster-Bandbreite**: DWA-A138 gibt "Pflaster mit offenen Fugen: 0,50" (definierter Wert) und "Sickersteine/Verbundsteine: 0,25". Leitfaden Bayreuth gibt eine breite Bandbreite 0,0–0,6. `simulation_params.py` verwendet 0,30 als Mittelwert — plausibel, aber mittelwertig.
- Das Dokument enthält keine Temperatur- oder LST-Daten — es ist rein hydrologisch. Die Verbindung zu Kühleffekten muss über [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] hergestellt werden.
- Keine Würzburg-spezifischen Bodendaten — LfU Bayern Bodentypen-WFS würde lokale kf-Werte liefern (als offenes TODO in [[wiki/simulation-logic.md]] bereits vermerkt).

## Wiki Pages Updated

- [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] — neu (diese Seite)
- [[wiki/concepts/entsiegelung]] — Abflussbeiwert-Tabelle um DWA-A138-Werte erweitert; Gründach-Zeilen ergänzt; DWA-A138 als Primärquelle hinzugefügt
- [[wiki/simulation-logic.md]] — DWA-A138 als Primärquelle für Abflussbeiwerte ergänzt; Asphalt-Diskrepanz dokumentiert
- [[wiki/overview.md]] — Quellzähler aktualisiert
- [[wiki/index.md]] — Source-Eintrag hinzugefügt
