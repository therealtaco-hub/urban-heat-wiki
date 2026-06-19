---
title: "Entsiegelung (Surface Unsealing)"
type: concept
tags: [entsiegelung, versickerung, grundwasser, temperatur, schwammstadt, bodenfunktionen]
sources: 4
updated: 2026-06-08
---

# Entsiegelung (Surface Unsealing)

Die vollständige oder teilweise Entfernung wasserundurchlässiger Bodenbeläge (Asphalt, Beton, Pflaster) zugunsten versickerungsfähiger oder begrünter Flächen. Neben der direkten Bepflanzung (Bäume, Parks) ist Entsiegelung die zweite Kernstrategie gegen urbane Wärmeinseln — mit zusätzlichen Effekten auf Versickerung, Grundwasser, Biodiversität und Hochwasserschutz.

## Quantitativer Kühlkoeffizient

**Zentralformel (Tervooren 2015, Potsdam, Cfb-Klima):**
> **ΔTempLST = −0,03°C × ΔVersiegelung [%]**

Jede 1% Reduktion der Versiegelungsfläche senkt die mittlere LST um **0,03°C**. Modellgüte: R²=0,75 (OLR), R²=0,80 (GWR). *(Source: [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]])*

**Vergleich mit Baumkronendeckung:**

| Maßnahme | Kühlkoeffizient | Quelle |
|----------|----------------|--------|
| +1% Baumkronendeckung (München, Mischgebiet) | −0,083°C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| +1% Baumkronendeckung (München, gesamt) | −0,069°C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| −1% Versiegelung (Potsdam) | −0,030°C | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| +10% Grünvolumen (Manchester) | −2,2 bis −2,5°C | via [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |

→ **Bäume kühlen rein temperaturmäßig ~2,3× stärker** pro Prozentpunkt als reine Entsiegelung.
→ Aber: Entsiegelung hat Mehrfacheffekte die Bäume allein nicht liefern.

## Mehrfachnutzen der Entsiegelung (über Temperatur hinaus)

1. **Versickerung**: Niederschlag versickert statt abzufließen → weniger Kanalbelastung bei Starkregen
2. **Grundwasserneubildung**: versickertes Wasser speist das Grundwasser
3. **Verdunstungskühlung** (Schwammstadt-Prinzip): gespeichertes Wasser verdunstet → latente Wärmebindung → Kühlung
4. **Biodiversität**: entsiegelte Böden ermöglichen Bodenbiologie, Insektenlebensräume
5. **Hochwasserschutz**: reduzierter Oberflächenabfluss bei Starkregenereignissen

## Versickerungsgrade nach Belagstyp

Die folgende Tabelle zeigt die **Abflussbeiwerte (Ψ)** nach DWA-A138 / LfU Bayern — die verbindliche Bayerische Ingenieursnorm für Versickerungsanlagen. Dies ist die Primärquelle für die in `backend/simulation_params.py` verwendeten Werte.

| Flächentyp | Belagsart | Ψ (Abflussbeiwert) |
|---|---|---|
| Straßen/Plätze | Asphalt, fugenloser Beton | **0,9** |
| Straßen/Plätze | Pflaster mit dichten Fugen | 0,75 |
| Straßen/Plätze | Fester Kiesbelag | 0,60 |
| Straßen/Plätze | Pflaster mit offenen Fugen | 0,50 |
| Straßen/Plätze | Lockerer Kiesbelag, Schotterrasen | 0,30 |
| Straßen/Plätze | Verbundsteine mit Fugen, Sickersteine | 0,25 |
| Straßen/Plätze | Rasengittersteine | **0,15** |
| Gründach (≤ 15°) | humusiert < 10 cm | 0,50 |
| Gründach (≤ 15°) | humusiert > 10 cm | 0,30 |
| Garten / Wiese | flaches Gelände | **0,0–0,1** |
| Garten / Wiese | steiles Gelände | 0,1–0,3 |

*(Source: [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] — DWA-A138 / LfU Bayern)*

Ergänzende Kostenangaben und eine breitere Bandbreite für Sickerpflaster (0,0–0,6) finden sich in [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] (Leitfaden Bayreuth 2024).

> Abflussbeiwert = Anteil des Niederschlags, der oberflächlich abfließt (nicht versickert). Kleiner Wert = mehr Versickerung + mehr Verdunstungspotenzial.

**Hinweis Asphalt-Diskrepanz:** DWA-A138 gibt Ψ = 0,9 für Asphalt/fugenloser Beton; `simulation_params.py` verwendet aktuell 0,95 (aus Leitfaden Bayreuth). Beide Werte liegen innerhalb der Bandbreite; DWA-A138 ist die Primärquelle.

## Entsiegelungstypen

- **Vollentsiegelung**: alle Sperr- und Deckschichten entfernt, standorttypischer Boden aufgebaut → maximale Bodenfunktionswiederherstellung *(Source: [[wiki/sources/uba-texte141-2021-entsiegelung]])*
- **Teilentsiegelung**: Belagswechsel (z.B. Asphalt → Sickerpflaster), Teilflächenentsiegelung, funktionale Entsiegelung (Abkopplung von der Kanalisation)
- **Schwammstadt**: blau-grüne Infrastruktur, die Regenwasser zurückhält, verdunstet und versickert

## Ausgangssituation Deutschland

- **45% der deutschen Siedlungs- und Verkehrsflächen sind versiegelt** (Stand 2024). *(Source: [[wiki/sources/leitfaden-flaechenentsiegelung-2024]])*
- Datenbasis für Würzburg: **Copernicus Imperviousness Layer** (frei verfügbar), IÖR-Monitor *(Source: [[wiki/sources/uba-texte141-2021-entsiegelung]])*

## Debates and Uncertainties

- Entsiegelungskoeffizient −0,03°C/% aus Potsdam (Cfb) — Übertragung auf Würzburg (Dfb) plausibel, nicht direkt validiert.
- GV und VG sind kreuzkorreliert: Grünvolumen und Versiegelungsgrad beeinflussen sich gegenseitig; Isolierung der reinen Entsiegelungswirkung ist methodisch schwierig.
- Entsiegelung ohne Bepflanzung kühlt deutlich weniger als Entsiegelung + Baumpflanzung kombiniert.

## Related Concepts

- [[wiki/concepts/impervious-surface]] — das Gegenteil von Entsiegelung
- [[wiki/concepts/green-infrastructure]] — oft kombiniert mit Entsiegelung
- [[wiki/concepts/evapotranspiration]] — der Kühlmechanismus, den Entsiegelung (re-)aktiviert
- [[wiki/concepts/land-surface-temperature]] — das gemessene Ergebnis

## Relevant Entities

- [[wiki/entities/wuerzburg]] — Zielgebiet
- [[wiki/entities/muenchen]] — hoher Versiegelungsgrad, politischer Kontext

## Sources

- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] — Kühlkoeffizient −0,03°C/%
- [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] — Primärquelle Abflussbeiwerte (DWA-A138 / LfU Bayern); Gründach-Werte; kf-Bodendaten
- [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] — Kosten, ergänzende Bandbreiten, Bayern-Kontext
- [[wiki/sources/uba-texte141-2021-entsiegelung]] — Rechtslage, Bodenfunktionen, nationale Datenbasis
