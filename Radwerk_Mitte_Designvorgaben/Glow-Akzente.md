# Glow-Akzente

Die Glow-Fläche ist ein dunkles „Display“ inmitten der hellen Seite – wie das Cockpit eines E-Bikes. Sie zeigt Daten, keine Werbung.

## Aufbau

1. Grund `nachtblau`, Radius `radius-lg`, Innenabstand `space-8` (mobil `space-6`).
2. Feines Linienraster: 1 px Linien in `cyan-strom` bei 8 % Deckkraft, Abstand 24 px.
3. Ein Hauptelement: Ring (Akku/Fortschritt), große Zahl oder Statuszeile – mit `shadow-glow-soft` dahinter.
4. Bis zu drei Kennzahlen: `data-label` in `ink-muted` (Glow), `data-value` in `ink` (Glow), links eine 2 px Linie in `cyan-strom`.
5. Optional eine Statuszeile unten: Punkt in `cyan-strom`, Mono-Text.

Innerhalb der Fläche gilt das Theme **Glow**: `interactive` wird automatisch Cyan, Text wird hell.

## Erlaubte Einsätze

| Ort | Inhalt |
| --- | --- |
| Startseite, Rechner | Ergebnis: „Ihre Monatsrate ca. 42 €“ + Hinweis „unverbindlich“ |
| Werkstatt | Statusabfrage per Auftragsnummer: „Abholbereit ab Donnerstag“ |
| E-Bikes | Technik eines Modells: Akku, Reichweite, Motor |
| Für Arbeitgeber | Ausblick Dienstrad-Portal (Stufe 2) – klar als „bald verfügbar“ markiert |

## Nicht erlaubt

- Mehr als eine Glow-Fläche pro Bildschirmhöhe.
- Glow für Formulare, Fließtext, Preise mit Vertragsbedingungen, Fehlermeldungen.
- Lila, Neonpink oder Verläufe in Fremdfarben; Leuchten nur in `cyan-strom`.
- Daueranimationen. Erlaubt ist ein einmaliges Aufbauen des Rings (max. 800 ms), abschaltbar per `prefers-reduced-motion`.
- Koralle in Glow nur als Button (`Termin wählen`), nie als Leuchtfarbe.
