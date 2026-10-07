# E-Auto vs. Diesel – Jahreskostenvergleich

Dashboard zum Vergleich der jährlichen Gesamtkosten eines Elektroautos mit einem Dieselauto.
Alles läuft im Browser – kein Server, keine Anmeldung, keine Datenübertragung.

**Live:** https://fbw159.github.io/eauto-diesel-vergleich/

## Was es kann

- **Zentraler Kennwert:** Einsparung des E-Autos gegenüber dem Diesel in €/Jahr
  (Einsparung = Jahreskosten Diesel − Jahreskosten E-Auto; positiv heißt: E-Auto günstiger)
- Aufschlüsselung nach Wertverlust, Versicherung, Energie/Kraftstoff und sonstigen Fixkosten
- Kosten je Monat und je km, Break-even-Fahrleistung
- Sensitivitätsanalysen: Fahrleistung, Verbrauch ±10/20 % (einzeln und kombiniert), Tornado-Diagramm
- Zu jedem Wert ein **?** mit Begründung; unten eine Liste aller Annahmen mit Quellen
- Szenarien als JSON speichern und laden (Beispiele im Ordner `szenarien/`)

## Benutzung

- Online über den Live-Link oben, oder
- Repository als ZIP herunterladen (**Code → Download ZIP**), entpacken und `index.html` doppelklicken.
  Chart.js liegt im Ordner `lib/`, die Diagramme funktionieren also auch offline.

Eingaben werden nur lokal im Browser gespeichert (localStorage).

## Berechnung

| Größe | Formel |
|---|---|
| Energiekosten E-Auto | Fahrleistung / 100 × Stromverbrauch × Strompreis |
| Kraftstoffkosten Diesel | Fahrleistung / 100 × Dieselverbrauch × Dieselpreis |
| Wertverlust | Wert × Kurve(Alter) × (40 % + 60 % × Fahrleistung / 15.000 km) |
| Gesamtkosten | Wertverlust + Versicherung + Energie/Kraftstoff + sonstige Fixkosten |
| Einsparung | Gesamtkosten Diesel − Gesamtkosten E-Auto |
| Break-even | (Fixkosten E − Fixkosten D) / (km-Kosten D − km-Kosten E) |

### Wertverlust aus Wert, Alter und Fahrleistung

Die Kurve gibt an, wie viel Prozent seines heutigen Werts ein Auto im kommenden Jahr bei durchschnittlich
15.000 km/Jahr verliert. 60 % davon hängen an den gefahrenen km, 40 % am Älterwerden.

| Alter | 0 (neu) | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8+ |
|---|---|---|---|---|---|---|---|---|---|
| E-Auto | 25 % | 17 % | 17 % | 13 % | 12 % | 11 % | 10 % | 9 % | 8 % |
| Diesel | 22 % | 12 % | 11 % | 10 % | 9 % | 8,5 % | 8 % | 7,5 % | 7 % |

Grundlage: Restwerte nach 1–5 Jahren von 75 / 66 / 59 / 53 / 48 % (kauf-oder-leasing.de) sowie nach 3 Jahren
51,5 % bei E-Autos und 61,1 % bei Diesel (Autohero). Kurve und Anteil lassen sich im Dashboard ändern.
Bei mehreren Jahren wird der Wertverlust Jahr für Jahr mit sinkendem Wert und steigendem Alter gerechnet.

## Basiswerte

| Parameter | E-Auto | Diesel | Art |
|---|---|---|---|
| Jährliche Fahrleistung | 30.000 km | 30.000 km | Vorgabe |
| Verbrauch | 17 kWh/100 km | 5,8 l/100 km | Vorgabe |
| Energiepreis | 0,25 €/kWh | 2,20 €/l | Vorgabe |
| Aktueller Fahrzeugwert | 21.600 € | 23.200 € | Annahme |
| Alter | 3 Jahre | 3 Jahre | Annahme |
| Versicherung | 780 €/Jahr | 720 €/Jahr | Annahme |
| Sonstige Fixkosten | 180 €/Jahr | 680 €/Jahr | Annahme |

Die Basiswerte sind Annahmen bzw. Vorgaben und keine aktuellen Marktpreise – bitte an die eigene Situation anpassen.

## Aufbau

```
index.html            Dashboard (HTML, CSS und JavaScript in einer Datei)
lib/chart.umd.min.js  Chart.js 4.5.1 (MIT-Lizenz, siehe lib/chartjs-LICENSE.md)
szenarien/*.json      Beispielszenarien zum Laden über „Szenario laden“
```
