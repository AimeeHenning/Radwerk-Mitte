# Radwerk Mitte

Designvorgaben für die neue Website (Stufe 1). Hell, klar und aufgeräumt wie ein großer Dienstrad-Anbieter – aber mit der Nähe einer Werkstatt vor Ort. Dunkle, leuchtende Akzentflächen zeigen sparsam, dass Radwerk den Schritt in die E-Mobilität und ins Digitale geht.

> **Haltung:** „Erst anschauen, dann sagen.“ Die Seite verspricht nichts, was sie nicht hält – und zeigt das in jedem Detail: klare Preise mit Hinweis „unverbindlich“, echte Ansprechpartner, echte Standorte.

## 1. Orientierung an JobRad – was wir übernehmen, was nicht

Radwerk orientiert sich am Aufbau von jobrad.org, weil Arbeitgeber und Beschäftigte dieses Muster vom Marktführer im Dienstrad-Leasing kennen. Wir übernehmen **Struktur und Muster**, nicht die Marke.

| Übernehmen (Muster) | Radwerk-eigene Ausprägung |
| --- | --- |
| Zielgruppen-Weiche ganz oben: Arbeitgeber / Beschäftigte / Privatkunden | Pill-Schalter im Hero, „Für Arbeitgeber“ ist vorausgewählt (B2B mit einem Klick erreichbar) |
| Vorteils- bzw. Leasing-Rechner prominent auf der Startseite | Rechner-Ergebnis als Glow-Fläche mit Monatsrate, Hinweis „unverbindlich“ |
| „So funktioniert’s“ in 3–4 nummerierten Schritten | Schritte enden bei der Übergabe **in der Filiale** – nicht beim Versand |
| Vertrauenszahlen und Kundenlogos | Regional: Klinikum, Stadtverwaltung, Pflegedienst; „seit 1989 in Kassel“ |
| Große, freundliche Fotos von Menschen auf dem Rad | Echte Mitarbeitende, echte Werkstatt in Kassel und Göttingen, keine Stockfotos |
| FAQ als Akkordeon vor dem Kontakt | FAQ entlastet den Kundenservice (heute eine Person) |
| Viel Weißraum, große Radien, Pill-Buttons | Hausfarben Radblau und Koralle statt fremder Markenfarben |

**Nicht übernehmen:** JobRads Farben, Logos, Illustrationsstil, Bildmotive und Formulierungen. Keine Portal-Optik mit Login (kommt erst in Stufe 2).

## 2. Farben

Grundregel: **80 % Hell, 15 % Radblau, 5 % Koralle und Glow.**

- `radblau` ist die Hausfarbe – Logo, primäre Buttons, Links, aktive Navigation.
- `koralle` ist das „Orange“ der Marke. Sie steht immer als **Fläche mit Nachtblau-Text**, nie als Schrift und nie mit weißem Text (zu wenig Kontrast). Pro Bildschirm höchstens ein Koralle-Element.
- `cyan-strom` gibt es **nur auf Nachtblau** – auf Weiß ist er unlesbar.
- `nachtblau` ist die Textfarbe auf Hell und der Grund aller Glow-Flächen.
- Sektionen wechseln zwischen `surface-page` und `surface-soft`; B2B-Inhalte dürfen `radblau-tint` als Hinterlegung bekommen.
- Status immer mit Icon **und** Wort: `status-ok` („Abholbereit“), `status-hinweis` („Verzögert – wir melden uns“). Nie Farbe allein.

Blau und Koralle unterscheiden sich in Helligkeit, nicht nur im Farbton – sie bleiben auch bei Farbfehlsichtigkeit unterscheidbar.

## 3. Glow-Akzentflächen (E-Mobilität & Digitales)

Die dunklen, leuchtenden Flächen sind das Signal „Radwerk wird digital“. Sie wirken nur, weil sie selten sind. Details im Abschnitt **Glow-Akzente**.

- **Höchstens eine Glow-Fläche pro Bildschirmhöhe**, höchstens zwei pro Seite.
- Nur für digitale oder elektrische Inhalte: Rechner-Ergebnis, Reparaturstatus, E-Bike-Technik (Akku, Reichweite, Motor), Online-Termin, Ausblick Dienstrad-Portal.
- Nie für Fließtext über drei Zeilen, Formulare, Preislisten, rechtliche Texte oder Fehlermeldungen.
- Grund `nachtblau`, feines Raster in Cyan bei 8 % Deckkraft, Leuchtkanten mit `shadow-glow`, Daten in der Mono-Schrift.

## 4. Typografie

- **Plus Jakarta Sans** (Google Fonts) für alles Sichtbare: freundlich-geometrisch, kräftig in den Überschriften (800), ruhig im Text (400).
- **JetBrains Mono** ausschließlich für Daten in Glow-Flächen und im Rechner-Ergebnis: Labels in Versalien (`data-label`), Werte groß (`data-value`).
- Fließtext 16/26, Zeilen max. 70 Zeichen (`text-max`). Überschriften linksbündig, nie zentrierte Textblöcke über zwei Zeilen.
- Sprache: Deutsch, per Sie, typografische Anführungszeichen „…“ und Apostroph ’.

## 5. Layout & Raster

- 12-Spalten-Raster, `container-max` 1200 px, Gap `space-6`. Mobil eine Spalte, Seitenrand `space-4`.
- Sektionsabstand `space-24` (Desktop) bzw. 64 px (mobil).
- Radien großzügig: Karten `radius-md`, Bildkacheln und Glow-Flächen `radius-lg`, Buttons `radius-pill`.
- Sticky Header (`header-height`) mit Logo, Zielgruppen-Navigation, Telefonnummer und dem Button „Angebot anfragen“.
- **Telefonnummer und beide Standorte (Kassel, Göttingen) stehen auf jeder Seite** – im Header (Telefon) und im Footer (beide Adressen, Öffnungszeiten).

## 6. Komponenten (Kurzregeln)

- **Button primär** – Radblau, weißer Text, Pill. Eine Hauptaktion pro Sektion („Angebot anfragen“, „Rate berechnen“).
- **Button akzent** – Koralle, Nachtblau-Text. Für die zweite konkrete Handlung („Termin wählen“).
- **Button sekundär** – weiß mit `border-strong`-Rand. Alles Weitere.
- **Zielgruppen-Kachel** – Foto oben (`radius-lg`), h3, ein Satz, Textlink mit Pfeil.
- **Schritte** – nummerierte Kreise in Radblau, max. vier Schritte.
- **Glow-Panel** – siehe Abschnitt 3.
- Fokus: 3 px Ring in `interactive` mit 2 px Abstand – auf Hell blau, in Glow cyan.

## 7. Bildsprache & Icons

- Echte Fotos aus Kassel und Göttingen: Mitarbeitende von Kunden auf dem Weg zur Arbeit, die Werkstatt, Heiner an der Montage. Tageslicht, natürliche Farben, Menschen zugewandt.
- Fotos nie mit Farbverlauf überlagern; Text steht neben dem Bild, nicht darauf.
- Icons: Outline, 1,75 px Strich, runde Enden, 24 px Raster (z. B. Lucide). In Hell `ink`, in Glow `cyan-strom`.
- Kein eigenes Logo-File in dieser Version: bis zur Lieferung des Logos steht der Schriftzug „radwerk mitte“ in Plus Jakarta Sans 800, „mitte“ in `radblau` (auf Dunkel `cyan-strom`).

## 8. Tonalität

Sachlich, hilfsbereit, per Sie. Kurze Sätze, konkrete Zusagen, keine Superlative.

- Gut: „Ihr Rad steht noch beim Hersteller und kommt am Donnerstag. Wir melden uns, sobald es fertig ist.“
- Nicht: „Das beste E-Bike-Erlebnis Deutschlands – jetzt revolutionär einfach!“

## 9. Barrierefreiheit (Pflicht)

Text mindestens 4,5:1, große Schrift und Bedienelemente 3:1 – in Hell **und** in Glow. Alle Animationen der Glow-Flächen respektieren `prefers-reduced-motion`. Mobil voll nutzbar, Touch-Ziele mindestens 44 × 44 px.
