# Design-Spec · Neue Website Radwerk Mitte (Stufe 1)

Stand: 19.10.2026 · Entwurf v1
Bezug: `PRD – Neue Website Radwerk Mitte.pdf`, `Radwerk_PRD_Kurzfassung.pdf`, `Radwerk_Mitte_Designvorgaben/`, [tech-spec.md](tech-spec.md)

Diese Spec übersetzt die fachlichen Ziele aus dem PRD in Gestaltungsentscheidungen. Sie ist der Gegenpart zur Tech-Spec: Die Tech-Spec sagt, wie die Seite gebaut wird – diese Spec sagt, wie sie aussieht, sich anfühlt und warum. Das verbindliche Detail-Regelwerk bleibt `Radwerk_Mitte_Designvorgaben/`; diese Datei fasst es ein und stellt den Bezug zu PRD-Zielen her, ohne es zu duplizieren.

## 1. Gestaltungsleitsatz

> „Erst anschauen, dann sagen.“ – Haltung des Hauses (`Firmensteckbrief-Radwerk-Mitte-BTA.pdf`).

Übersetzt auf Design: Die Seite verspricht nichts, was sie nicht hält. Keine Superlative, keine Marketing-Übertreibung, keine Preise ohne Hinweis „unverbindlich“, echte Ansprechpartner und echte Standorte statt Stockfotos. Jede Gestaltungsentscheidung wird daran gemessen, ob sie dieses Versprechen sichtbar macht oder ihm widerspricht.

## 2. Design-Ziele aus dem PRD

| PRD-Ziel | Design-Konsequenz |
| --- | --- |
| Mehr B2B-Aufträge gewinnen | Eigene, gleichwertig gestaltete Zielgruppen-Ebene für Arbeitgeber – nicht als Unterseite versteckt |
| B2B-Angebot sichtbar machen | Zielgruppen-Schalter im Hero, „Für Arbeitgeber“ vorausgewählt, B2B mit einem Klick erreichbar |
| Kosten online selbst abschätzen | Leasing-Rechner prominent auf der Startseite, Ergebnis optisch als „Display“ (Glow-Fläche) abgesetzt |
| Anfrageweg ohne E-Mail | Formular wirkt wie der naheliegende nächste Schritt (Pill-Button, nicht wie Pflichtformular versteckt) |
| Kundenservice entlasten | FAQ und Statusabfrage so gestaltet, dass sie als vollwertige Antwort wirken, nicht als Verlegenheitslösung |
| Verlässlichkeit zeigen, modern auftreten | Helles, aufgeräumtes Grundlayout + sparsame Glow-Akzente als Signal „digital, aber bodenständig“ |
| Regional sichtbarer werden | Referenzen/Kundenlogos (Klinikum, Stadtverwaltung, Pflegedienst) sichtbar im Trust-Bereich |

## 3. Strukturelles Vorbild: JobRad

Radwerk orientiert sich strukturell an jobrad.org, weil Arbeitgeber und Beschäftigte dieses Muster vom Marktführer kennen. Übernommen wird **Struktur**, nicht Marke:

- Zielgruppen-Weiche ganz oben (Arbeitgeber/Beschäftigte/Privatkunden)
- Rechner prominent auf der Startseite
- „So funktioniert's“ in nummerierten Schritten
- Vertrauenszahlen/Kundenlogos
- FAQ als Akkordeon vor dem Kontakt

Bewusst **nicht** übernommen: JobRads Farben, Logo, Illustrationsstil, Bildmotive, Formulierungen, Portal-Login-Optik. Details und die vollständige Gegenüberstellung: `Radwerk_Mitte_Designvorgaben/README.md`, Abschnitt 1.

## 4. Visuelle Sprache (Kurzfassung)

Kanonische Werte: `Radwerk_Mitte_Designvorgaben/tokens.json`. Hier nur die Regeln, die jede Entscheidung leiten:

- **Farbverteilung 80 % Hell / 15 % Radblau / 5 % Koralle + Glow.** Radblau ist Haupt-/Markenfarbe (Buttons, Links, Navigation). Koralle ist immer Fläche mit Nachtblau-Text – nie Schrift, nie mit Weiß kombiniert, max. ein Koralle-Element pro Bildschirm. Cyan-Strom nur auf Nachtblau.
- **Glow-Flächen** (dunkles „Cockpit-Display“) sind das alleinige Signal für Digitales/Elektrisches: Rechner-Ergebnis, Reparaturstatus, E-Bike-Technik, Online-Termin. Max. eine pro Bildschirmhöhe, max. zwei pro Seite, nie für Fließtext, Formulare, Preislisten, Rechtstexte oder Fehlermeldungen. Details: `Glow-Akzente.md`.
- **Typografie**: Plus Jakarta Sans für alles Sichtbare (kräftig in Überschriften, ruhig im Fließtext); JetBrains Mono ausschließlich für Daten in Glow-Flächen. Fließtext max. 70 Zeichen Zeilenlänge.
- **Layout**: 12-Spalten-Raster, `container-max` 1200 px, großzügige Radien, Pill-Buttons, sticky Header mit Telefonnummer.
- **Bildsprache**: echte Fotos aus Kassel/Göttingen, Tageslicht, keine Stockfotos, keine Farbverläufe über Fotos.
- **Icons**: Outline, 1,75 px Strich, 24-px-Raster (z. B. Lucide).

Vollständiges Regelwerk inkl. Begründungen: `README.md` Abschnitte 2–7.

## 5. Seitenstruktur Startseite

Verbindliche Reihenfolge und Begründung je Sektion in `Seitenaufbau.md` (11 Sektionen: Header, Hero, Vertrauensleiste, Leasing-Rechner, So funktioniert's, Zielgruppen-Kacheln, Referenz, Werkstatt & Status, FAQ, Kontakt, Footer). Designentscheidung dahinter: Glow kommt genau zweimal vor (Rechner, Werkstatt/Status) und nie direkt hintereinander – das hält die Seltenheit des Signals ein, die seine Wirkung ausmacht.

## 6. Komponenten

Spezifiziert mit Regeln (`README.md` je Komponente) und lauffähiger Vorschau (`preview.html`) in `components/`: `Button`, `AudienceCard`, `GlowPanel`, `Steps`, `Cover`.

- **Button primär** (Radblau/Weiß): eine Hauptaktion pro Sektion.
- **Button akzent** (Koralle/Nachtblau): zweite konkrete Handlung.
- **Button sekundär** (Weiß/Rand): alles Weitere.
- **Zielgruppen-Kachel**: Foto, h3, ein Satz, Textlink mit Pfeil.
- **Schritte**: nummerierte Kreise, max. vier.
- **Glow-Panel**: siehe Abschnitt 4.

**Bekannte Lücke:** `components/*/preview.html` referenziert `../../tokens.css`, das im Designvorgaben-Ordner noch fehlt (nur `tokens.json` liegt vor). Vorschauen lassen sich erst nach Generierung dieser Datei korrekt im Browser prüfen – siehe auch [tech-spec.md](tech-spec.md) Abschnitt 4. Kein Logo-File vorhanden; bis zur Lieferung gilt der Schriftzug-Workaround aus `README.md` Abschnitt 7.

## 7. Tonalität

Deutsch, formelles Sie, typografische Anführungszeichen „…“ und Apostroph ’. Sachlich, hilfsbereit, kurze Sätze, konkrete Zusagen, keine Superlative.

- Gut: „Ihr Rad steht noch beim Hersteller und kommt am Donnerstag. Wir melden uns, sobald es fertig ist.“
- Nicht: „Das beste E-Bike-Erlebnis Deutschlands – jetzt revolutionär einfach!“

Status wird immer mit Icon **und** Wort gezeigt (z. B. „Abholbereit“, „Verzögert – wir melden uns“), nie über Farbe allein.

## 8. Barrierefreiheit (Pflicht, nicht verhandelbar)

- Textkontrast mindestens 4,5:1, große Schrift/Bedienelemente mindestens 3:1 – in Hell **und** Glow.
- `prefers-reduced-motion` wird respektiert; einzige erlaubte Animation ist ein einmaliges Aufbauen des Glow-Rings (max. 800 ms).
- Touch-Ziele mindestens 44 × 44 px.
- Blau und Koralle unterscheiden sich in Helligkeit, nicht nur im Farbton, damit sie auch bei Farbfehlsichtigkeit unterscheidbar bleiben.
- Telefonnummer und beide Standorte (Kassel, Göttingen) stehen auf jeder Seite (Header: Telefon; Footer: Adressen, Öffnungszeiten).

## 9. Offene Design-Fragen

Aus den „Offenen Fragen an Merle“ der PRD, hier design-seitig zugespitzt:

1. Reicht eine Auffrischung in Blau/Koralle, oder wird die visuelle Sprache grundsätzlich neu gedacht? (PRD stellt das explizit zur Diskussion, weil der heutige Auftritt „verwirrend“ wirkt.)
2. Ist die Navigation B2B/Privatkunden/Werkstatt auf den ersten Blick unterscheidbar genug – Nutzertest vor Launch nötig?
3. Wie viele Freigaberunden für Entwürfe, und wer entscheidet außer Merle Vogelsang mit?
4. Welche Fotos/Personen stehen für die geforderte „echte Mitarbeitende, echte Werkstatt“-Bildsprache zur Verfügung, und wann werden sie geliefert?
5. Logo: Wann liegt die finale Logo-Datei vor, damit der Schriftzug-Workaround abgelöst werden kann?

## 10. Nicht-Ziele (Design, Stufe 1)

- Kein Rebranding – Blau und Koralle bleiben gesetzt, nur der Auftritt wird moderner.
- Keine Portal-Optik mit Login (Stufe 2).
- Keine Illustrationen/Bildmotive im JobRad-Stil oder einer fremden Marke.
- Kein Custom-Rad-Konfigurator-Interface.
