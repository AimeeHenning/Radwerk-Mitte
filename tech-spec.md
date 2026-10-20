# Tech-Spec · Neue Website Radwerk Mitte (Stufe 1)

Stand: 19.10.2026 · Entwurf v1
Bezug: `PRD – Neue Website Radwerk Mitte.pdf`, `Radwerk_PRD_Kurzfassung.pdf`, `Radwerk_Mitte_Designvorgaben/`

Diese Spec übersetzt die fachlichen Anforderungen aus dem PRD in eine technische Umsetzung. Sie ist der Gegenpart zu den Designvorgaben: Das Design-Regelwerk sagt, wie die Seite aussieht und sich anfühlt – diese Spec sagt, wie sie gebaut, betrieben und angebunden wird.

## 1. Ausgangslage

- Bestehende Seite: WordPress, veraltet, zeigt B2B-Angebot kaum, nur Anfragen per E-Mail.
- Budget: ca. 150.000 €, Erweiterung nach Rücksprache möglich.
- Team: Kundenservice bleibt bei einer Person (Amara Osei) – die Lösung muss ohne zusätzliche Stellen funktionieren.
- Content-Pflege: Svenja Kowalczyk (E-Commerce/Marketing) pflegt Texte und Bilder selbst, ohne Programmierkenntnisse.
- **Technik ist laut PRD ausdrücklich nicht gesetzt**: *"Wir analysieren die bestehende WordPress-Seite per Fragebogen, bevor wir die Technik festlegen."* Diese Spec macht einen begründeten Vorschlag (Abschnitt 3), der nach dem Fragebogen/Audit bestätigt oder revidiert wird.
- Livegang-Ziel: vor Saisonstart Frühjahr 2027.

## 2. Architekturüberblick

Drei Ebenen, lose gekoppelt, damit Stufe 2 (App, Arbeitgeber-Portal) später andocken kann, ohne Stufe 1 umzubauen:

1. **Content- & Darstellungsebene** – öffentliche Website (Seiten, Texte, Bilder, Design-System aus `Radwerk_Mitte_Designvorgaben/`).
2. **Funktionsebene** – eigenständige Module mit klar begrenztem Zweck: Leasing-Rechner, Terminbuchung, Statusabfrage, Anfrageformular, FAQ/Chat.
3. **Integrationsebene** – Anbindung an bestehende Systeme (Werkstattplanung, Warenwirtschaft, Leasingpartner-Konditionen, E-Mail-Weiterleitung, externer Onlineshop).

```
                    ┌─────────────────────────────┐
                    │   Öffentliche Website        │
                    │  (Seiten, CMS-Inhalte,        │
                    │   Design-Tokens)              │
                    └───────────────┬───────────────┘
                                    │
        ┌───────────────┬──────────┼──────────┬───────────────┐
        ▼               ▼          ▼          ▼               ▼
  Leasing-Rechner   Terminbuchung  Statusabfrage  Anfrage-    FAQ-Chat
  (Client-Berechnung,  │               │         formular   (regelbasiert/
   keine Datenhaltung) │               │           │          Wissensbasis)
                       ▼               ▼           ▼
                 ┌─────────────┐ ┌───────────┐ ┌─────────┐
                 │Werkstatt-    │ │Warenwirt- │ │E-Mail-   │
                 │planung (API) │ │schaft(API)│ │Weiterltg.│
                 └─────────────┘ └───────────┘ └─────────┘
```

Wichtig: Der **Leasing-Rechner rechnet clientseitig** mit vom Leasingpartner gelieferten Konditionswerten (keine Übertragung personenbezogener Gehaltsdaten an einen Server) – siehe Abschnitt 6.1.

## 3. Technologie-Stack (Vorschlag, zur Bestätigung nach Technik-Audit)

| Ebene | Vorschlag | Begründung |
| --- | --- | --- |
| CMS | Headless CMS mit deutschsprachigem, einfachem Editor (z. B. ein System mit Block-Editor und Rollen für Marketing/Content) | Svenja muss Texte/Bilder ohne Entwickler ändern können; headless hält Frontend-Flexibilität für spätere App (Stufe 2) |
| Frontend | Serverseitig gerendertes Framework mit statischer Generierung für Inhaltsseiten (z. B. Next.js/Nuxt-artig) | Gute Performance/SEO für B2B-Entscheider, die vor dem Erstkontakt recherchieren; wiederverwendbare Design-Tokens aus `tokens.json`/`tokens.css` als CSS-Variablen |
| Hosting | Managed Hosting/CDN mit EU-Rechenzentrum | DSGVO-Anforderung, Lastspitzen zum Saisonstart abfedern |
| Formular-/Funktionslogik | Serverless Functions oder schlanker Anwendungsserver für Terminbuchung, Statusabfrage, Formularversand | Entkoppelt von CMS-Deploys, einfacher an Werkstattplanung/Warenwirtschaft anzubinden |
| Analytics | Cookieless/datensparsames Webanalyse-Tool | Pflichtkriterium „datenschutzkonform“ aus der PRD-Kurzfassung |

**Offen bis Audit:** Ob die bestehende WordPress-Instanz migriert, als Headless-CMS weiterbetrieben oder vollständig abgelöst wird, hängt vom Fragebogen-Ergebnis zur Altsystem-Architektur ab (Plugins, Datenbestand, SEO-Historie, Shop-Anbindung). Diese Spec geht von einer **Ablösung** aus, weil die PRD die Seite als „veraltet“ beschreibt; das ist eine Annahme, keine Festlegung.

## 4. Seiten & Komponenten

Referenz: `Radwerk_Mitte_Designvorgaben/Seitenaufbau.md` (11 Sektionen der Startseite) und `components/` (Button, AudienceCard, GlowPanel, Steps, Cover).

Technisch werden die Sektionen aus Seitenaufbau.md als wiederverwendbare Komponenten umgesetzt, nicht als Einzelseiten-Markup:

- `Header` (sticky, Zielgruppen-Navigation, Telefonnummer, CTA)
- `Hero` (Zielgruppen-Schalter: Arbeitgeber/Beschäftigte/Privatkunden)
- `TrustBar`, `Testimonial`, `AudienceTiles`
- `LeasingCalculator` (Glow-Panel-Variante)
- `HowItWorks` (Steps-Komponente, max. 4 Schritte)
- `WorkshopStatus` (Terminbuchung + Statusabfrage, Glow-Panel-Variante)
- `FAQAccordion`
- `ContactForm` (mit Pflichtfeld Kategorie)
- `Footer` (beide Standorte, Öffnungszeiten, Telefon, Partner, Rechtliches)

Jede Komponente bindet die Design-Tokens aus `tokens.json`/`tokens.css` ein (Farben, Typografie, Radien, Schatten) – siehe `README.md` der Designvorgaben für die Farbregeln (80/15/5, Koralle nie als Text, Cyan nie auf Hell).

**Fehlende Abhängigkeit:** Die Komponentenvorschauen in `components/*/preview.html` referenzieren `../../tokens.css`, das im Repo noch **nicht vorhanden** ist (nur `tokens.json`). Vor Implementierungsbeginn muss `tokens.css` aus `tokens.json` generiert oder geliefert werden.

## 5. Kernfunktionen (Module)

### 5.1 Leasing-Rechner
- Eingaben: Radpreis, Bruttogehalt.
- Ausgabe: geschätzte monatliche Belastung, Darstellung als Glow-Fläche, Pflichthinweis „unverbindlich“ (siehe Akzeptanzkriterium PRD).
- Berechnungslogik läuft clientseitig; Konditionswerte (Leasingfaktor, Verskontierung o. ä.) kommen als Konfigurationsdaten vom Leasingpartner – **offene Frage an Radwerk**: welche Partner/Konditionen genau (siehe PRD „Offene Fragen“).
- Keine Speicherung der eingegebenen Gehaltsdaten; keine Übertragung an Dritte.
- Erfolgsmessung: Nutzungszähler (Rechner geöffnet / Berechnung ausgeführt) für die PRD-Metrik „Nutzung des Rechners“.

### 5.2 Werkstatttermin-Buchung
- Ablauf in **höchstens 3 Schritten** (Akzeptanzkriterium): Standort wählen (Kassel/Göttingen) → Zeitfenster wählen → Kontaktdaten + Bestätigung.
- Nach Buchung: automatische Bestätigung (E-Mail) und Erinnerung vor dem Termin.
- Bei Terminverschiebung durch die Werkstatt: automatische Nachricht an den Kunden **vor** dem ursprünglich zugesagten Termin (Akzeptanzkriterium Kurzfassung).
- Erfordert Anbindung an die Werkstattplanung (Abschnitt 6.2) für verfügbare Zeitfenster je Standort.

### 5.3 Statusabfrage (Reparaturstatus)
- Eingabe: Auftragsnummer.
- Ausgabe: aktueller Status als Glow-Fläche mit Icon + Wort (z. B. „Abholbereit“, „Verzögert – wir melden uns“) – nie Farbe allein (Barrierefreiheits-Pflicht).
- Erfordert Leseanbindung an Werkstattplanung/Warenwirtschaft (Abschnitt 6.2–6.3).
- Kein Login nötig – Zugriff ausschließlich über Auftragsnummer (plus ggf. Zusatzprüfung wie Name/PLZ gegen Enumeration, siehe Abschnitt 8).

### 5.4 B2B-/Kontaktanfrage
- Formular mit **Pflichtfeld Kategorie**: B2B-Angebot, Werkstatt, Bestellung, Sonstiges.
- Leitet je nach Kategorie an die zuständige Person weiter (Dilan Aydın für B2B, Amara Osei für Service).
- Absender erhält sofortige Eingangsbestätigung (Akzeptanzkriterium).
- B2B-Formular erfasst zusätzlich Firmengröße/Bedarf (Anforderung Dilan Aydın in PRD).
- Keine neue Support-Software (Nicht-Ziel) – Versand per E-Mail an bestehende Postfächer, kein Ticketsystem.

### 5.5 FAQ & Chat
- FAQ als Akkordeon, 6–8 häufigste Fragen, inhaltlich mit Kundenservice abgestimmt.
- Chat beantwortet ausschließlich FAQ-artige Standardfragen und übergibt alles andere an das Team (E-Mail/Formular) – **kein** beratender, verkaufender oder terminzusagender Chat (explizites Nicht-Ziel der PRD-Kurzfassung).

### 5.6 Shop-Verweis
- Kein eigener Onlineshop in Stufe 1. Verlinkung auf den bestehenden externen Shop.
- Falls im Shop-System Verfügbarkeit je Filiale abrufbar ist, Anzeige „welches Rad in welcher Filiale verfügbar ist“ als reine Leseanbindung (Lesezugriff, kein Checkout).

## 6. Integrationen

| System | Richtung | Zweck | Status |
| --- | --- | --- | --- |
| Werkstattplanung | Lesen/Schreiben | Verfügbare Zeitfenster, Terminbuchung, Statusabfrage | Anbindbar laut PRD-Annahme – **System/API noch nicht benannt, zu klären** |
| Warenwirtschaft | Lesen | Reparaturstatus, Lagerbestand je Filiale | Anbindbar laut PRD-Annahme – **System/API noch nicht benannt, zu klären** |
| Leasingpartner | Lesen (Konfigurationsdaten) | Konditionswerte für den Rechner | Laut PRD-Annahme liefert der Partner die Werte – **welcher Partner, welches Format: offene Frage** |
| E-Mail-Versand | Schreiben | Formularweiterleitung, Bestätigungen, Erinnerungen | Bestehende Postfächer, kein neues Ticketsystem (Nicht-Ziel) |
| Externer Onlineshop | Verweis/ggf. Lesen | Verlinkung, optional Verfügbarkeitsanzeige | Shop bleibt unverändert (Annahme PRD) |
| Bestehende WordPress-Seite | Migration | Content-Übernahme, SEO-Umleitung (Redirects) | Umfang hängt vom Technik-Audit ab |

Alle drei markierten Integrationen (Werkstattplanung, Warenwirtschaft, Leasingpartner) sind in der PRD nur als **Annahme** benannt, nicht als konkretes System. Diese Spec erfindet keine Schnittstellennamen oder -formate – das ist in Abschnitt 11 als offene Frage aufgeführt.

## 7. Datenmodell (fachlich, vorläufig)

- **Anfrage**: Kategorie, Kontaktdaten, Freitext, ggf. Firmengröße/Bedarf (B2B), Zeitstempel, Status (eingegangen/weitergeleitet).
- **Termin**: Standort, Zeitfenster, Kontaktdaten, Status (gebucht/bestätigt/verschoben/wahrgenommen), verknüpfte Erinnerung.
- **Auftrag/Status**: Auftragsnummer, Status-Label (mit Icon-Zuordnung), optionales Abholdatum.
- **Referenz**: Kundenname/-logo, Zitat, Foto, Freigabe-Flag (nur mit Einwilligung veröffentlichbar).
- **FAQ-Eintrag**: Frage, Antwort, Kategorie, Pflegeverantwortliche Person.

Alle Inhaltsdaten (Texte, Bilder, Referenzen, FAQ) liegen im CMS und sind von Svenja Kowalczyk ohne Entwicklerhilfe pflegbar. Transaktionsdaten (Anfrage, Termin, Auftragsstatus) liegen in der Funktionsebene/den angebundenen Systemen, nicht im CMS.

## 8. Nicht-funktionale Anforderungen

- **Barrierefreiheit**: WCAG-Kontrastwerte 4,5:1 (Text) / 3:1 (große Schrift, Bedienelemente) in Hell **und** Glow-Theme; `prefers-reduced-motion` wird respektiert (max. 800 ms einmalige Glow-Ring-Animation, sonst keine Dauerbewegung); Touch-Ziele mindestens 44×44 px; Status nie nur über Farbe.
- **Mobil**: Alle Seiten und Funktionen (Rechner, Terminbuchung, Statusabfrage, Formular) vollständig auf dem Smartphone nutzbar (Akzeptanzkriterium).
- **Datenschutz/DSGVO**: Keine Übertragung von Gehaltsdaten aus dem Rechner an einen Server; Statusabfrage so gestaltet, dass Auftragsnummern nicht durch einfaches Durchprobieren fremde Daten offenlegen (z. B. Kombination mit Name/PLZ oder Rate-Limiting); Analytics datensparsam/cookieless oder mit Einwilligungsbanner; Hosting mit EU-Rechenzentrum.
- **Performance**: Schnelle Ladezeiten für B2B-Entscheider, die die Seite vor Erstkontakt prüfen; statisches Rendering für Inhaltsseiten, serverseitige Logik nur für die Funktionsmodule.
- **Content-Pflege ohne Programmierer**: CMS mit Rollen- und Rechtekonzept für Marketing/Content, keine Deploys nötig für Text-/Bildänderungen.
- **Betrieb ohne zusätzliches Personal**: FAQ, Chat-Vorsortierung und automatisierte Bestätigungen/Erinnerungen entlasten den einzigen Kundenservice-Mitarbeiter (Amara Osei) messbar (PRD-Metrik „weniger Standardanfragen“).
- **Messbarkeit**: Seit Launch keine Vergleichswerte vorhanden (PRD-Annahme) – Analytics muss ab Tag 1 sauber laufen, damit B2B-Anfragen/Monat, Rechnernutzung und Absprungrate als Baseline erfasst werden.

## 9. Design-System-Anbindung

Die technische Umsetzung übernimmt `Radwerk_Mitte_Designvorgaben/` 1:1 als Quelle der Wahrheit:
- Farb-, Typografie-, Abstands- und Schatten-Tokens aus `tokens.json` als CSS-Variablen (sobald `tokens.css` vorliegt, siehe Abschnitt 4).
- Glow-Flächen-Regeln aus `Glow-Akzente.md`: max. eine Glow-Fläche pro Bildschirmhöhe, max. zwei pro Seite, nur für Rechner-Ergebnis, Reparaturstatus, E-Bike-Technik, Online-Termin – technisch als eigene Komponentenvariante mit eigenem Farbthema (`Glow`) umgesetzt, nicht als Spezialfall der hellen Komponenten.
- Kein Logo-File vorhanden – bis zur Lieferung gilt der Schriftzug-Workaround aus `README.md` Abschnitt 7.

## 10. Testing & Qualitätssicherung

- Visuelle/funktionale Abnahme je Komponente gegen `components/*/preview.html` und die jeweiligen `README.md`.
- Kontrastprüfung automatisiert (Hell- und Glow-Theme) als Teil der CI.
- End-to-End-Tests für die drei kritischen Pfade: Terminbuchung (≤ 3 Schritte), Statusabfrage, B2B-Anfrageformular inkl. Weiterleitung und Eingangsbestätigung.
- Abnahme durch Merle Vogelsang vor Launch (laut PRD Freigabe-Instanz).

## 11. Offene technische Fragen

Direkt aus den „Offenen Fragen an Merle“ der PRD abgeleitet, hier technisch zugespitzt:

1. Welches System läuft hinter „Werkstattplanung“ und „Warenwirtschaft“ – existiert bereits eine API, oder muss eine gebaut werden?
2. Welcher Leasingpartner liefert die Rechner-Konditionen, in welchem Format (manuelle Pflege vs. automatisierter Abgleich)?
3. Welche Service-Level-Agreement-Inhalte dürfen öffentlich angezeigt werden (z. B. Rückmeldezeiten im Formular)?
4. Wird die bestehende WordPress-Seite abgelöst oder bleibt sie als Backend bestehen (abhängig vom Technik-Fragebogen)?
5. Soll ein API-Vorbereitungsschnitt für das spätere Arbeitgeber-Portal (Stufe 2) schon jetzt im Datenmodell berücksichtigt werden, oder erst bei Bedarf?
6. Existiert eine Schnittstelle zum externen Onlineshop für Filial-Verfügbarkeit, oder bleibt es bei einem reinen Link?

## 12. Nicht-Ziele (technisch, Stufe 1)

- Keine native App.
- Kein Arbeitgeber-Portal mit Login (Datenmodell so halten, dass es sich später ergänzen lässt, aber nicht bauen).
- Kein Custom-Rad-Konfigurator.
- Kein Austausch von Warenwirtschaft oder Shopsystem – nur Anbindung/Verlinkung.
- Kein Chat mit Beratungs-, Verkaufs- oder Terminzusage-Funktion.
- Kein Rebranding – Blau/Koralle bleiben, nur Umsetzung in neuem Design-System.
