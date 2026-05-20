---
title: "Quantitative Kühleffekte — Vergleichstabelle"
type: overview
tags: [kühleffekte, lst, bäume, vergleich, quantitativ, synthese]
sources: 9
updated: 2026-05-20
---

# Quantitative Kühleffekte — Vergleichstabelle

Synthese aller quantitativen Kühleffekte aus dem Wiki. Bei neuen Ingests aktualisieren.

---

## A — Baumkronendichte vs. LST (Regressionskoeffizienten)

| Kontext | Kühleffekt | Einheit | R² | Quelle |
|---|---|---|---|---|
| München, gesamtes Stadtgebiet | −0,069 | °C pro 1% Baumkronendeckung | hoch | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| München, Mischgebiete (Mixed) | −0,083 | °C pro 1% Baumkronendeckung | n/a | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| München, Wohngebiete (Residential) | −0,083 | °C pro 1% Baumkronendeckung | n/a | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| München, Verkehrsflächen (Traffic) | n/a | — | 0,61 | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| München, Erholungsflächen (Recreational) | −0,038 | °C pro 1% Baumkronendeckung | 0,41 | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |

> Praktische Lesart: +20% Baumkronendeckung in einem Mischgebiet → ~−1,66°C mittlere LST.

---

## B — Bäume vs. versiegelte Fläche (absolute LST-Differenz)

| Kontext | Kühleffekt | Einheit | Bedingung | Quelle |
|---|---|---|---|---|
| Zentraleuropa (inkl. Deutschland), Sommer | 8 – 12 | K | Bäume vs. Stadtgewebe | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| Südeuropa, Sommer | 0 – 4 | K | Bäume vs. Stadtgewebe (ET-limitiert) | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| Bäume vs. baumlose Grünflächen | 2 – 4× effektiver | Faktor | Gleiche Region, Sommer | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| München: Mixed vs. Recreational | ~4,5 | °C LST-Differenz | Median ~39°C vs. ~34,5°C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |

---

## C — Baumverlust vs. Temperaturanstieg (kausaler Effekt)

| Kontext | Effekt | Einheit | Bedingung | Quelle |
|---|---|---|---|---|
| Worcester MA, Baumverlust 2008–2015 | +1 bis +6 | °C LST-Anstieg (Peak) | UTC-Verlust pro Fläche | [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] |
| Worcester MA, Verlängerung Hitzesaison | +15 | Tage | UTC-Verlust vs. stabile Flächen | [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] |

---

## D — Einzelbaum-Kühlleistung (Energiebilanz)

| Kontext | Kühleffekt | Einheit | Bedingung | Quelle |
|---|---|---|---|---|
| 20m hoher, dichtbelaubter Baum | bis 40.000 | kWh/Jahr | Schatten + Evapotranspiration | [[wiki/sources/gegen-hitze-kuehlleistung-baum]] |
| Äquivalenter Klimaanlagenersatz | ~16.000 | €/Jahr | Bezogen auf Energiepreis | [[wiki/sources/gegen-hitze-kuehlleistung-baum]] |

---

## E — Wasseroberflächen

| Kontext | Kühleffekt | Einheit | Jahr | Quelle |
|---|---|---|---|---|
| Wasserflächen, Hawassa (Sub-Sahara) | −2,1 | °C (Max-Temp) | 1991 | [[wiki/sources/reta-roba-hawassa-vegetation-lst]] |
| Wasserflächen, Hawassa | −1,2 | °C (Max-Temp) | 2005 | [[wiki/sources/reta-roba-hawassa-vegetation-lst]] |
| Wasserflächen, Hawassa | −0,5 | °C (Max-Temp) | 2021 | [[wiki/sources/reta-roba-hawassa-vegetation-lst]] |

> Abnehmende Wirkung über Zeit — vermutlich durch wachsende Versiegelung im Umfeld. Übertragbarkeit auf Deutschland eingeschränkt (anderes Klima).

---

## F — Schwellenwerte (unter denen kein Kühleffekt eintritt)

| Parameter | Schwellenwert | Effekt darunter | Quelle |
|---|---|---|---|
| NDVI | < 0,4 | kein signifikanter LST-Kühleffekt | [[wiki/sources/li-et-al-urban-form-lst-xgboost]] |
| Landschaftsdiversität (SHDI) | < 0,65 | kein Kühleffekt durch Diversität | [[wiki/sources/li-et-al-urban-form-lst-xgboost]] |
| Gebäudedichte | > 20% (Sommer) | Wärmeeffekt | [[wiki/sources/li-et-al-urban-form-lst-xgboost]] |

> NDVI-Schwellenwert aus chinesischen Städten — Validierung für Würzburg ausstehend.

---

## G — Artenauswahl: Trockentoleranz vs. Kühlleistung

| Baumtyp | Transpiration | Einheit | Differenz | Quelle |
|---|---|---|---|---|
| Feuchtigkeitsadaptiert (LB3): *Tilia cordata*, *Acer platanoides*, *Carpinus betulus* | 0,19 | kg H₂O m⁻² Tag⁻¹ | Referenz | [[wiki/sources/klimabaeume-fuer-die-stadt]] |
| Trockenheitstolerant (LB6): *Tilia tomentosa*, *Acer campestre*, *Ostrya carpinifolia* | 0,17 | kg H₂O m⁻² Tag⁻¹ | −11% | [[wiki/sources/klimabaeume-fuer-die-stadt]] |

---

## Übertragbarkeit auf Würzburg

| Befund | Relevanz |
|---|---|
| −0,069°C pro 1% Baumkrone (München) | **Direkt übertragbar** — gleiche Methodik, gleiche Region, Würzburger Forscher |
| 8–12 K Kühleffekt Bäume (Zentraleuropa) | **Direkter Benchmark** — Würzburg liegt klimatisch in dieser Zone |
| −0,083°C/% in Mischgebieten | **Planungsrelevant** — typisch die heißesten und baumärmsten Zonen |
| NDVI-Schwellenwert 0,4 | **Methodisch relevant** für Identifikation wirksamer Eingriffsflächen |
| Trockentoleranz −11% Transpiration | **Planungsrelevant** für Baumartenauswahl |

---

## H — Parkanlagen (Park Cool Island Effekt)

Quelle: [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]] — Literaturreview, 185 Quellen.

| Fläche | Kühleffekt (Lufttemp.) | Tageszeit | Klimazone | Quelle (in Stangl) |
|--------|----------------------|-----------|-----------|-------------------|
| 2,4 ha | −1,7°C | — | — | Upmanis et al. 1998 |
| 3,6 ha | −2,0°C | — | — | Upmanis et al. 1998 |
| 156 ha | −5,9°C | — | — | Upmanis et al. 1998 |
| 1,96 ha | bis −4,8°C | tagsüber | — | Vidrih & Medved 2013 |
| 6 ha | −3,3 bis −3,8°C | tagsüber | Griechenland (Csa) | Skoulika et al. 2014 |
| 14 ha | −0,5 bis −2,0°C | tagsüber | Schweden (Cfb) | Jansson et al. 2007 |
| 23 ha | −3,5°C (max −6°C) | nächtlich | USA (Wüste) | Chow et al. 2011 |
| 41,9 ha | −6,8°C | tagsüber | Japan (Cfa) | Cao et al. 2010 |
| 111 ha | −1,1°C (max −4°C) | nächtlich | UK (Cfb) | Doick et al. 2014 |

**Schwellenwerte:**
- Mindestgröße für merklichen Kühleffekt: **>2–3 ha**
- Maximale Effizienz bei: **~40 ha** — darüber nimmt Wirkung ab
- Grünraumergänzung (Simulation): bis **−2°C lokal**, −0,5°C regional

> Mitteleuropa (Cfb/Dfb, Würzburg-nächste Zone): Schweden (Cfb) zeigt −0,5 bis −2,0°C für 14 ha — vorsichtiger Benchmark.

---

## I — Gründächer

Quelle: [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]]

| Typ | Lufttemperaturreduktion | Bedingung |
|-----|------------------------|-----------|
| Extensives Gründach | **0,4–0,7°C** | Simulation, Hongkong (Peng & Jim 2013) |
| Intensives Gründach | **0,5–1,7°C** | Simulation, Hongkong (Peng & Jim 2013) |

- Kühleffekt reicht vom Dach bis in den **Fußgängerbereich** (nicht nur Gebäudeebene)
- Energieeinsparung Klimaanlage: **58,9% Sommer / 4,2% Winter** (Coma et al. 2017)

> Einschränkung: Werte aus Hongkong (Cwa/Cfa) — für Würzburg (Cfb/Dfb) tendenziell etwas geringer.

---

## J — Vertikalbegrünung (Fassaden)

Quelle: [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]]

**Wichtig**: Diese Werte gelten für die **Wandoberfläche**, nicht für die Lufttemperatur.

| Standort/Klima | Exposition | Oberflächenkühlung |
|---------------|------------|-------------------|
| Österreich **(Dfb)** | S | **−15,0°C** |
| Österreich (Dfb), Autobahn | SO | bis **−18,9°C** |
| Niederlande **(Cfb)** | W | **−5,0°C** |
| Italien (Csa) | N,S,O,W | −9,0°C |
| China (Cfa) | W | −20,8°C |
| Singapur (Af) | — | −11,6°C |
| Spanien (Csa) | S | −31,9°C |

**Mitteleuropa-relevante Bandbreite (Cfb/Dfb): −5 bis −19°C Wandoberfläche**

Innenraumtemperatur: **−1,9°C (Nord) bis −2,7°C (Süd)** (Yang et al. 2018)
Klimaanlagenenergie: −12% bis −42% (Pan et al. 2018)

---

## K — Thermischer Komfort (PET-Reduktion durch Bäume)

Quelle: [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]]

| Maßnahme | PET-Reduktion | Jahreszeit |
|----------|--------------|-----------|
| Baumgruppen (Einzelbäume) | −12 bis −16°C PET | — |
| Hohe Kronendichte | bis −18°C PET | Sommer |
| Hohe Kronendichte | bis −10°C PET | Winter |
| Bäume im Fußgängerbereich | −1°C Lufttemperatur | Sommer |
| Park (95% Beschattung vs. unbeschattet) | >3°C Lufttemperatur | tagsüber |

> PET (Physiological Equivalent Temperature) beschreibt die gefühlte Temperatur unter Berücksichtigung Strahlung, Wind und Feuchte — relevanter für Hitzestress als LST.

---

## L — Entsiegelung (Versiegelungsreduktion vs. LST)

Quelle: [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] | Ergänzung: [[wiki/sources/leitfaden-flaechenentsiegelung-2024]], [[wiki/sources/uba-texte141-2021-entsiegelung]]

**Zentralformel:**
> **ΔTempLST = −0,03°C × ΔVersiegelung [%]**
> Jede 1% Reduktion der Versiegelungsfläche → −0,03°C mittlere LST. Modellgüte: R²=0,75 (OLR), R²=0,80 (GWR). Kontext: Potsdam (Cfb), heißer Sommertag 2010.

**Vergleich Entsiegelung vs. Baumpflanzung:**

| Maßnahme | Kühlkoeffizient | Quelle |
|----------|----------------|--------|
| −1% Versiegelung (Potsdam) | −0,030°C LST | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| +1% Baumkronendeckung (München, gesamt) | −0,069°C LST | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| +1% Baumkronendeckung (München, Mischgebiet) | −0,083°C LST | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| +10% Grünvolumen | −2,2 bis −2,5°C | Manchester via [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |

→ **Bäume kühlen ~2,3× stärker** pro Prozentpunkt als reine Entsiegelung (temperaturmäßig).
→ Aber: Entsiegelung aktiviert Versickerung, Grundwasserneubildung und Biodiversität — Mehrfachnutzen.

**Abflussbeiwerte nach Belagstyp (Leitfaden Bayreuth 2024):**

| Belag | Abflussbeiwert | Grünanteil | Materialkosten |
|-------|---------------|-----------|---------------|
| Rasendecke | 0,0–0,1 | 100% | 70–260 €/m² |
| Rasenwabe / Rasengitter | 0,15 | 40–90% | 35–45 €/m² |
| Schotterrasen | 0,3 | 20–30% | 20–30 €/m² |
| Sickerpflaster | 0,0–0,6 | 0% | 130–270 €/m² |
| Lehm/Kies/Splitt | 0,4 | 0% | 15–20 €/m² |
| Asphalt (Referenz) | ~0,95 | 0% | — |

> Abflussbeiwert = Anteil des Niederschlags, der abfließt (nicht versickert). Kleiner = mehr Verdunstung = mehr Kühlpotenzial.

> Koeffizient aus Potsdam (Cfb) — Übertragung auf Würzburg (Dfb) plausibel, nicht direkt validiert.

---

## Fehlende Quantitaten (Stand 2026-05-20)

- Würzburg-spezifische LST-Werte — noch keine lokale Quelle vorhanden
- Gesundheitliche Schwellenwerte (ab welcher Temperatur steigt Mortalität) — keine Quelle im Wiki
- Mitteleuropa-spezifische Gründach-/Fassadenwerte — bisherige Zahlen aus Asien/Mittelmeer
