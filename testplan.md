# Testplan · Neue Website Radwerk Mitte (Stufe 1)

Stand: 20.10.2026 · Entwurf v1
Bezug: `PRD – Neue Website Radwerk Mitte.pdf`, `Radwerk_PRD_Kurzfassung.pdf`, `Radwerk_Mitte_Designvorgaben/`, [design.md](design.md), [index.html](index.html)

Dieser Testplan prüft die aktuelle Startseiten-Umsetzung (`index.html`) gegen die Akzeptanzkriterien der PRD und das verbindliche Regelwerk aus `Radwerk_Mitte_Designvorgaben/`. Er ist kein Lastenheft – er setzt Ziele und Spec als gegeben voraus und beschreibt, wie geprüft wird, ob die Umsetzung sie erfüllt.

## 1. Testgegenstand

**In Scope:** die elf Sektionen der Startseite (Header, Hero, Vertrauensleiste, Leasing-Rechner, So funktioniert's, Zielgruppen-Kacheln, Referenz, Werkstatt & Status, FAQ, Kontakt, Footer) als statisches Frontend inkl. Client-seitiger Logik (Audience-Switch, Rechner, Terminassistent, Statusabfrage, Formularvalidierung).

**Out of Scope (Stufe 1, lt. PRD „Nicht-Ziele"):** eigener Onlineshop, Partnerportal mit Login, Custom-Rad-Konfigurator, neue Support-Software/CMS-Backend. Ebenfalls außerhalb dieses Testplans, weil technisch noch nicht vorhanden:

- echter Versand der Formulardaten (Kontaktformular, Terminbuchung) – aktuell nur clientseitige Bestätigung ohne Übertragung;
- echte Anbindung der Statusabfrage an die Werkstattplanung – aktuell feste Demo-Datensätze (`RW-48213`, `RW-50871`);
- Analytics/Tracking für Absprungrate und Anfragenzahl – im Code nicht vorhanden;
- Inhalte der Rechtsseiten (Impressum, Datenschutz, AGB) – Links sind Platzhalter (`href="#"`).

Diese Punkte sind in Abschnitt 8 als Blocker für die vollständige Abnahme der PRD-Akzeptanzkriterien aufgeführt.

## 2. Teststrategie

| Testart | Fokus |
| --- | --- |
| Funktional | Jede interaktive Komponente verhält sich wie spezifiziert (Rechner, Terminassistent, Statusabfrage, Formulare, Navigation) |
| Barrierefreiheit | Kontrast, Tastaturbedienung, Screenreader, Touch-Ziele, `prefers-reduced-motion`, Status nie nur über Farbe |
| Responsive / Cross-Device | Smartphone, Tablet, Desktop; Breakpoints lt. CSS (640/768/900/1024 px) |
| Browser-Kompatibilität | Aktuelle Versionen Chrome, Safari, Firefox, Edge |
| Design-Konformität | Farbdisziplin (80/15/5-Regel), Glow-Regeln, Typografie, Komponentenregeln aus `README.md`/`Glow-Akzente.md` |
| Content & Tonalität | Deutsch, Sie-Form, typografische Anführungszeichen, keine Superlative, Status mit Icon + Wort |
| Nicht Teil dieser Stufe | Performance-Messung, echtes A/B-Tracking, Backend-/E-Mail-Zustellung – siehe Abschnitt 8 |

## 3. Testumgebung

- **Browser:** Chrome, Safari, Firefox, Edge (jeweils aktuelle Version)
- **Viewports:** ≤480 px (Smartphone, inkl. Ring-Layout-Umbruch im Rechner), 768 px (Tablet), 900–1023 px (Nav-Umbruch Mobile→Desktop), ≥1024 px, ≥1440 px
- **Hilfsmittel:** VoiceOver (macOS/iOS) oder NVDA stichprobenartig, Tastatur-only-Durchlauf, axe DevTools oder Lighthouse für Kontrast/ARIA, Browser-Einstellung „Reduce Motion" aktiviert/deaktiviert
- **Testdaten:** siehe Abschnitt 7

## 4. Rollen

| Rolle | Person | Prüffokus |
| --- | --- | --- |
| Freigabe (Go-Live) | Merle Vogelsang | Gesamtabnahme, Design-Freigabe |
| Fachliche Prüfung B2B/Rechner | Dilan Aydın | Leasing-Rechner, B2B-Formularfeld „Firmengröße/Bedarf" |
| Fachliche Prüfung Service | Amara Osei | FAQ-Inhalte, Kontaktformular-Kategorien, Statusabfuhr |
| Inhaltliche Pflege (ab Stufe mit CMS) | Svenja Kowalczyk | nicht in Stufe 1 testbar, da kein CMS vorhanden |
| Technische Durchführung | QA/Umsetzungsteam | alle Testfälle in Abschnitt 6 |

## 5. Einstiegs- und Freigabekriterien

**Einstiegskriterium:** `index.html` lässt sich lokal öffnen, `Radwerk_Mitte_Designvorgaben/tokens.css` ist vorhanden und wird geladen (Pfadverweis in Zeile 8 von `index.html`).

**Freigabekriterium:** alle Testfälle mit Priorität „Hoch" bestanden, alle PRD-Akzeptanzkriterien aus Abschnitt 8 entweder erfüllt oder als bekannter Stufe-1-Blocker dokumentiert und von Merle Vogelsang akzeptiert.

## 6. Testfälle

### 6.1 Header & Navigation

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-01-01 | Telefonnummer immer sichtbar | Seite auf allen Viewports laden | Telefonlink „0561 807 630" im Header sichtbar und als `tel:`-Link anklickbar | Hoch |
| TF-01-02 | Hauptnavigation Desktop | Viewport ≥900 px | Nav-Links „Für Arbeitgeber / Für Beschäftigte / Werkstatt / E-Bikes & Shop" sichtbar, Anker scrollen zur richtigen Sektion | Hoch |
| TF-01-03 | Mobile Menü öffnen/schließen | Viewport <900 px, Burger-Button klicken | Menü öffnet (`aria-expanded="true"`), Label wechselt zu „Menü schließen"; Klick auf Link schließt Menü wieder | Hoch |
| TF-01-04 | Sticky Header | Seite scrollen | Header bleibt oben fixiert, Inhalt verdeckt nichts Wichtiges | Mittel |
| TF-01-05 | CTA „Angebot anfragen" im Header | Button klicken | Scrollt zu `#kontakt` | Hoch |

### 6.2 Hero & Zielgruppen-Schalter

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-02-01 | Standardzustand | Seite laden | „Für Arbeitgeber" ist vorausgewählt (`aria-pressed="true"`) – B2B ist mit einem Klick/direkt sichtbar | Hoch |
| TF-02-02 | Umschalten Arbeitgeber → Beschäftigte | Button „Für Beschäftigte" klicken | Headline, Lead-Text und beide CTAs wechseln auf Beschäftigten-Variante; `aria-pressed` wechselt korrekt | Hoch |
| TF-02-03 | Umschalten → Privatkunden | Button „Privatkunden" klicken | Inhalt wechselt auf Privatkunden-Variante; beide CTAs zeigen auf Werkstatt-Sektion | Hoch |
| TF-02-04 | Nur ein aktiver Zustand | Mehrfach zwischen allen drei Optionen wechseln | Immer genau ein Button mit `aria-pressed="true"` | Mittel |
| TF-02-05 | Bildalternativtext | Screenreader auf Hero-Foto-Platzhalter | `aria-label` beschreibt Bildinhalt sinnvoll (kein „Foto" ohne Kontext) | Mittel |

### 6.3 Vertrauensleiste

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-03-01 | Referenzlogos sichtbar | Sektion ansehen | Klinikum, Stadtverwaltung, Pflegedienst als Kundenlogos/-namen erkennbar | Mittel |
| TF-03-02 | Umbruch bei schmalem Viewport | Viewport <480 px | Fakten und Logos brechen lesbar um, keine Überlappung | Niedrig |

### 6.4 Leasing-Rechner (Glow-Fläche)

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-04-01 | Berechnung Standardwerte | Seite laden, keine Eingabe ändern | Monatsrate wird direkt angezeigt (nicht leer), Werte für Radpreis/Laufzeit/Ersparnis stimmen mit Formel überein | Hoch |
| TF-04-02 | Live-Neuberechnung | Radpreis auf 6.000 € ändern | Rate, Ring-Füllstand und Kennzahlen aktualisieren sich sofort ohne Klick auf „Rate berechnen" | Hoch |
| TF-04-03 | Grenzwerte Radpreis | Werte 500 € (Min) und 12.000 € (Max) eingeben | Keine negative/NaN-Anzeige, Ring-Darstellung bleibt sinnvoll begrenzt (min. sichtbarer Bogen) | Hoch |
| TF-04-04 | Grenzwerte Gehalt (Staffelschwellen) | Gehalt 3.499 €, 3.500 €, 5.499 €, 5.500 € eingeben | Ersparnisanzeige wechselt an den Schwellen 28 %/32 %/38 % exakt wie in `ersparnisProzent()` | Mittel |
| TF-04-05 | Laufzeitwechsel | Laufzeit 24/36/48 Monate wählen | Monatsrate sinkt/steigt erwartungsgemäß, Anzeige „Laufzeit" aktualisiert sich | Hoch |
| TF-04-06 | Hinweis „unverbindlich" vorhanden | Rechner-Ergebnis ansehen | Textzeile mit „Unverbindliche Beispielrechnung" ist sichtbar (PRD-Akzeptanzkriterium) | Hoch |
| TF-04-07 | Kein Datenversand | Netzwerk-Tab beobachten, Rechner bedienen | Keine Request mit Gehalts-/Preisdaten an einen Server – Hinweistext „läuft ausschließlich im Browser" stimmt | Hoch |
| TF-04-08 | `aria-live` auf Ergebnis | Screenreader, Eingabe ändern | Änderung der Rate wird vom Screenreader angesagt (`aria-live="polite"` auf `.glow-panel`) | Mittel |
| TF-04-09 | Eingabe leeren/ungültig | Radpreis-Feld leeren | Keine JS-Fehlermeldung in der Konsole, Anzeige fällt auf 0 €/sinnvollen Default zurück statt „NaN €" | Hoch |

### 6.5 So funktioniert's

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-05-01 | Schrittanzahl und Reihenfolge | Sektion ansehen | Genau vier nummerierte Schritte, enden bei „Übergabe vor Ort" (nicht Versand) – lt. Designvorgabe | Mittel |
| TF-05-02 | Layout-Umbruch | Viewport <768 px | Schritte stehen untereinander statt in 4 Spalten | Niedrig |

### 6.6 Zielgruppen-Kacheln

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-06-01 | Drei Kacheln vorhanden | Sektion ansehen | Arbeitgeber, Beschäftigte, Werkstatt je mit Foto, Überschrift, Satz, Pfeil-Link | Mittel |
| TF-06-02 | B2B-Kachel hervorgehoben | Sektion ansehen | Arbeitgeber-Kachel hat sichtbaren Radblau-Rahmen (`is-b2b`) | Niedrig |
| TF-06-03 | Links führen zur richtigen Sektion | Jeden Kachel-Link klicken | „Angebot anfragen" → `#kontakt`, „Rate berechnen" → `#rechner`, „Termin wählen" → `#werkstatt` | Hoch |

### 6.7 Referenz/Testimonial

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-07-01 | Mindestens eine Geschäftskundenreferenz sichtbar | Sektion ansehen | Zitat + Zuordnung „Personalabteilung, regionales Klinikum" vorhanden (PRD-Akzeptanzkriterium) | Hoch |
| TF-07-02 | Tonalität | Zitat lesen | Sachlich, konkret, keine Superlative | Niedrig |

### 6.8 Werkstatt & Status (Glow-Fläche)

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-08-01 | Terminassistent – Schritt 1→2→3 | Standort wählen, „Weiter" klicken, Zeitfenster wählen, „Weiter" klicken | Schrittanzeige und sichtbarer Schritt wechseln korrekt, „Zurück" funktioniert ebenso | Hoch |
| TF-08-02 | Pflichtfelder Schritt 3 | Name/E-Mail leer lassen, „Termin bestätigen" klicken | Browser-native Validierung verhindert Absenden (HTML `required`) | Hoch |
| TF-08-03 | Bestätigungstext nach Absenden | Formular gültig ausfüllen und absenden | Bestätigungszeile mit Standort, Zeitfenster und Hinweis auf E-Mail-Bestätigung erscheint, `role="status"` meldet dies Screenreadern | Hoch |
| TF-08-04 | Statusabfrage – Treffer „ok" | `RW-48213` eingeben, „Status abrufen" | Ergebnis „Abholbereit ab Donnerstag" mit Haken-Icon **und** Text (nicht nur Farbe) | Hoch |
| TF-08-05 | Statusabfrage – Treffer „Hinweis" | `RW-50871` eingeben | Ergebnis „Verzögert – wir melden uns vor dem Termin" mit Warn-Icon **und** Text | Hoch |
| TF-08-06 | Statusabfrage – kein Treffer | Unbekannte Nummer eingeben | Hinweis „Keine Übereinstimmung … Amara Osei kontaktieren", kein JS-Fehler | Mittel |
| TF-08-07 | Statusabfrage – leere Eingabe | Leer absenden | Hinweis „Bitte Auftragsnummer eingeben." | Mittel |
| TF-08-08 | Groß-/Kleinschreibung | `rw-48213` (klein) eingeben | Treffer wird trotzdem gefunden (`toUpperCase()`) | Niedrig |
| TF-08-09 | Glow-Konformität dieser Sektion | Sektion betrachten | Nur die Statusabfrage ist als Glow-Fläche gestaltet, der Terminassistent links ist eine helle Karte – max. eine Glow-Fläche pro Bildschirmhöhe eingehalten | Mittel |

### 6.9 FAQ

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-09-01 | Akkordeon öffnet/schließt | Jede Frage anklicken | `<details>` öffnet einzeln, Chevron dreht sich (bzw. bleibt bei „Reduce Motion" starr) | Mittel |
| TF-09-02 | Tastaturbedienbarkeit | Mit Tab zu Fragen navigieren, Enter/Space zum Öffnen | Funktioniert ohne Maus | Hoch |
| TF-09-03 | Inhaltliche Abdeckung Standardfragen | Alle sieben Fragen lesen | Deckt Leasing-Dauer, Datenschutz Rechner, Terminbuchung, Terminverschiebung, Statusabfrage, Betriebsgröße, Online-Shop ab – mit Kundenservice (Amara Osei) abzustimmen | Mittel |

### 6.10 Kontaktformular

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-10-01 | Kategorie ist Pflichtfeld | Formular ohne Kategorie absenden | `reportValidity()` verhindert Absenden, Fokus springt zum Feld | Hoch |
| TF-10-02 | Kategorien vollständig | Dropdown öffnen | Optionen „B2B-Angebot, Werkstatt, Bestellung, Sonstiges" lt. PRD-Akzeptanzkriterium vorhanden | Hoch |
| TF-10-03 | Bedingtes Feld „Firmengröße/Bedarf" | Kategorie „B2B-Angebot" wählen | Feld „Firmengröße/Bedarf" erscheint; bei anderer Kategorie bleibt es versteckt | Hoch |
| TF-10-04 | Pflichtfelder Name/E-Mail | Nur Kategorie ausfüllen, absenden | Validierung verlangt Name und gültiges E-Mail-Format | Hoch |
| TF-10-05 | Erfolgsbestätigung | Formular vollständig und gültig ausfüllen, absenden | Bestätigungstext „Danke für Ihre Anfrage …" erscheint, per `role="status"` angekündigt | Hoch |
| TF-10-06 | Rückmeldezeit kommuniziert | Rechte Spalte lesen | Hinweis „innerhalb eines Werktags", Zuständigkeiten Dilan Aydın/Amara Osei benannt | Hoch |
| TF-10-07 | Alternative Telefonnummer | Rechte Spalte prüfen | `tel:`-Link vorhanden und identisch mit Header-Nummer | Mittel |

### 6.11 Footer

| ID | Testfall | Schritte | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- | --- |
| TF-11-01 | Beide Standorte vollständig | Footer ansehen | Kassel und Göttingen je mit Adresse, Telefonnummer, Öffnungszeiten (PRD-Akzeptanzkriterium) | Hoch |
| TF-11-02 | Rechtslinks vorhanden (Platzhalter geprüft) | Impressum/Datenschutz/AGB anklicken | Links existieren; **bekannte Lücke:** führen aktuell zu `#` statt echten Seiten – vor Launch zu ersetzen | Hoch (Blocker) |
| TF-11-03 | Hinweis „fiktive Übungsfirma" | Footer-Note lesen | Vorhanden – vor echtem Launch zu entfernen/anzupassen | Hoch (Blocker) |

## 7. Testdaten

| Zweck | Daten |
| --- | --- |
| Statusabfrage Treffer „ok" | `RW-48213` |
| Statusabfrage Treffer „Hinweis" | `RW-50871` |
| Statusabfrage ohne Treffer | z. B. `RW-00000` |
| Rechner – Randwerte | Radpreis 500 € / 12.000 €; Gehalt 999 € / 1.000 € / 3.499 € / 3.500 € / 5.499 € / 5.500 € / 15.000 € |
| Kontaktformular – ungültige E-Mail | `max@` (ohne Domain) |

## 8. Abgleich mit den PRD-Akzeptanzkriterien

| PRD-Akzeptanzkriterium | Abgedeckt durch | Status |
| --- | --- | --- |
| Dienstrad-Leasing für Unternehmen mit einem Klick von der Startseite erreichbar | TF-02-01, TF-06-03 | Testbereit |
| Leasing-Rechner gibt nach Radpreis/Bruttogehalt die Monatsrate aus, mit Hinweis „unverbindlich" | TF-04-01–TF-04-09 | Testbereit |
| Anfrageformular verlangt Kategorie und leitet an zuständige Person weiter | TF-10-01–TF-10-06 | UI testbar; **Weiterleitung an Person nicht prüfbar**, da kein Versand implementiert (siehe oben) |
| FAQ deckt häufigste Standardfragen ab, abgestimmt mit Kundenservice | TF-09-03 | Inhaltlich mit Amara Osei abzustimmen, noch offen |
| Mindestens eine Referenz eines Geschäftskunden sichtbar | TF-07-01 | Erfüllt |
| Telefonnummer und beide Standorte auf jeder Seite | TF-01-01, TF-11-01 | Erfüllt (aktuell nur eine Seite/Startseite existiert) |
| Link zum externen Onlineshop funktioniert | – | **Fehlt:** Kein Link zum externen Shop in `index.html` gefunden (FAQ erwähnt ihn nur textlich) – zu ergänzen und dann zu testen |
| Design nutzt Blau und Orange, wirkt modern, freigegeben durch Merle | TF-Design-01–TF-Design-06 (Abschnitt 9) | Technisch testbar, Freigabe durch Merle steht aus |
| Alle Seiten funktionieren auf dem Smartphone | TF-Responsive-01–TF-Responsive-03 (Abschnitt 9) | Testbereit |
| Absprungrate und Anfragenzahl ab Launch messbar | – | **Blocker:** kein Tracking/Analytics im Code vorhanden |

## 9. Übergreifende Testfälle

### 9.1 Barrierefreiheit

| ID | Testfall | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- |
| TF-A11Y-01 | Textkontrast Hell-Theme | Alle Fließtexte ≥4,5:1, große Schrift/Buttons ≥3:1 (axe/Lighthouse) | Hoch |
| TF-A11Y-02 | Textkontrast Glow-Theme | Cyan-Strom-Text und Mono-Daten in Glow-Flächen ≥4,5:1 bzw. 3:1 | Hoch |
| TF-A11Y-03 | Touch-Ziele | Alle Buttons, Choice-Pills, Nav-Toggle ≥44×44 px | Hoch |
| TF-A11Y-04 | Tastaturbedienung komplett | Gesamte Seite ohne Maus bedienbar (Skip-Link, Nav, Switch, Rechner, Assistent, FAQ, Formulare) | Hoch |
| TF-A11Y-05 | Fokus sichtbar | `:focus-visible`-Ring auf allen interaktiven Elementen erkennbar | Hoch |
| TF-A11Y-06 | `prefers-reduced-motion` | Mit aktivierter Einstellung: kein Smooth-Scroll, keine Chevron-Drehung, Ring-Animation deaktiviert | Mittel |
| TF-A11Y-07 | Status nie nur über Farbe | Statusabfrage-Ergebnisse und Terminbestätigung je mit Icon **und** Wort geprüft | Hoch |
| TF-A11Y-08 | Skip-Link funktioniert | Tab-Taste beim Laden drücken, Enter | Fokus springt zu `#main`, Link vorher sichtbar | Mittel |
| TF-A11Y-09 | Screenreader-Ansage Zielgruppen-Schalter | Mit Screenreader durch `role="group"` navigieren | Gruppe und gedrückter Zustand werden korrekt angesagt | Mittel |
| TF-A11Y-10 | Alternativtexte Bildplatzhalter | Alle `.photo-placeholder`/`.img`-Elemente prüfen | `aria-label`/sichtbarer Text beschreibt den späteren Bildinhalt sinnvoll | Niedrig |

### 9.2 Design-Konformität

| ID | Testfall | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- |
| TF-Design-01 | Farbverteilung | Visuelle Prüfung der Startseite | Eindruck entspricht ca. 80 % Hell / 15 % Radblau / 5 % Koralle+Glow, kein Element mit weißem Text auf Koralle | Mittel |
| TF-Design-02 | Koralle nur als Fläche | Alle `.btn-accent`-Vorkommen prüfen | Immer Koralle-Hintergrund mit Nachtblau-Text, nie als reine Schriftfarbe | Hoch |
| TF-Design-03 | Cyan-Strom nur auf Nachtblau | Seite nach `cyan-strom`-Verwendung durchsuchen | Kommt ausschließlich innerhalb von `.glow-panel`/`[data-theme="glow"]` vor | Hoch |
| TF-Design-04 | Maximal zwei Glow-Flächen, nie direkt hintereinander | Ganze Seite scrollen | Glow nur bei Rechner (Sektion 4) und Statusabfrage (Sektion 8), dazwischen mind. drei andere Sektionen | Hoch |
| TF-Design-05 | Typografie | Schriftarten prüfen | Plus Jakarta Sans für alles Sichtbare, JetBrains Mono ausschließlich in Glow-Daten (Ring-Wert, Kennzahlen, Statuszeilen) | Mittel |
| TF-Design-06 | Telefonnummer/Standorte auf jeder Seite | Header und Footer parallel prüfen | Erfüllt wie in TF-01-01/TF-11-01 | Hoch |

### 9.3 Responsive/Cross-Device

| ID | Testfall | Erwartetes Ergebnis | Priorität |
| --- | --- | --- | --- |
| TF-Responsive-01 | Smartphone-Portrait (375 px) | Vollständige Seite ohne horizontales Scrollen, Ring-Layout im Rechner wird einspaltig, Navigation im Burger-Menü | Hoch |
| TF-Responsive-02 | Tablet (768 px) | Steps-Grid 4-spaltig, Audience-Grid mehrspaltig, Navigation noch im Burger-Menü (<900 px) | Mittel |
| TF-Responsive-03 | Desktop (≥1024/1440 px) | Container zentriert bei `container-max`, Hauptnavigation sichtbar, Inhalte nicht übermäßig gestreckt | Mittel |

## 10. Bekannte Lücken (Blocker für vollständige PRD-Abnahme)

1. **Kein echter Formularversand:** Kontaktformular und Terminassistent zeigen nur clientseitige Bestätigungen; die PRD-Anforderung „leitet an die zuständige Person weiter" ist serverseitig noch nicht umgesetzt/testbar.
2. **Kein Analytics/Tracking:** Die PRD-Erfolgsmessung (B2B-Anfragen/Monat, Rechnernutzung, Absprungrate, abgeschlossene Formularanfragen) ist ohne Tracking-Implementierung nicht messbar.
3. **Fehlender Shop-Link:** Die PRD verlangt einen funktionierenden Link zum externen Onlineshop; im aktuellen `index.html` wird der Shop nur in der FAQ erwähnt, nicht verlinkt.
4. **Platzhalter-Rechtsseiten:** Impressum/Datenschutz/AGB verlinken auf `#`.
5. **Demo-Hinweis im Footer:** „Fiktive Übungsfirma" – vor echtem Launch zu entfernen.
6. **Nur eine Seite vorhanden:** B2B-Unterseite, E-Bike-Produktseiten etc. aus der Navigation (`#zielgruppen` etc.) sind Anker auf derselben Startseite, keine eigenständigen Unterseiten – zu klären, ob das für Stufe 1 so vorgesehen ist.

Diese Punkte sind keine Fehler der aktuellen Umsetzung, sondern Hinweise, was vor der Freigabe durch Merle Vogelsang noch zu ergänzen bzw. mit ihr abzustimmen ist.
