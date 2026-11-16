# Schachclub HDH – DHBW Schachportal

**Webplattform für die Schach-Community an der DHBW Heidenheim.** Ein nicht-kommerzielles Studienprojekt im Rahmen der Vorlesung *Webentwicklung / Wirtschaftsinformatik* (Dozent: Jens Reiner), entwickelt von **Adrian, Jeremy, Nicolas & Nils**.

Das Portal verbindet Studierende für wöchentliche Trainingsabende nach der Vorlesung (mittwochs ab 18:00 Uhr in Raum A4.14), interne Schnellschach- und Blitzturniere sowie die Grundlagen des Schachspiels – umgesetzt mit reinem, barrierefreiem HTML5 und CSS3 komplett ohne JavaScript.

---

## Ansehen

- **Lokal:** `index.html` direkt im Browser öffnen (Doppelklick). Es wird kein Build-Schritt, kein Webserver und kein JavaScript benötigt.
- **Online:** Bereitgestellt als statische Website über **GitHub Pages** (Repository: `Donoperek/PROJEKT-SCHACHCLUB`).

---

## Struktur

```text
PROJEKT-SCHACHCLUB/
├── README.md                              ← Projektdokumentation
├── index.html                             ← Startseite mit Einleitung, Bereichskacheln & CTA
├── projekt.github/
│   └── copilot-instructions.md            ← Verbindliche Projekt- & Barrierefreiheitsvorgaben
├── pages/
│   ├── ueber-uns.html                     ← Vorstellung des Clubs, Trainingsformat & Gemeinschaft
│   ├── rangliste.html                     ← Schnellschach- & Blitz-Elo-Rangliste + Statistik-Sidebar
│   ├── termine.html                       ← Anstehende Events & regelmäßige Termine (Theoriephase)
│   ├── lernen.html                        ← Interaktives 8×8-Brett, Regel-Karussell & Lernlinks
│   ├── anmeldung.html                     ← FAQ-Akkordeon, Schnuppertraining & Anmeldeformular
│   ├── kontakt.html                       ← Teamvorstellung mit Fotos, Kontaktdaten & Formular
│   ├── impressum.html                     ← Impressum (Beispieldaten für das Studienprojekt)
│   └── datenschutz.html                   ← Datenschutzerklärung (GitHub Pages, lokale Fonts)
├── css/
│   ├── style.css                          ← Einziger CSS-Einstiegspunkt (importiert alle 4 Module)
│   ├── base.css                           ← Lokale @font-face-Schriften, Design-Tokens, Dark/Light-Mode, A11y
│   ├── layout.css                         ← Responsive Header (Logo-Wechsel, Menü, Theme & Sprache), Footer
│   ├── components.css                     ← Startseiten-Kacheln (.kategorie) & Anmelde-Button
│   └── pages.css                          ← Seitenspezifische Layouts (Rangliste, Brett, Formulare, Karten)
└── assets/
    ├── fonts/                             ← Lokal eingebundene WOFF2-Dateien (Montserrat 400, 600, 700)
    ├── icons/
    │   ├── logo_transparent_weiss.png     ← Logo-Variante für den Dark Mode
    │   └── logo_transparent.png           ← Logo-Variante für den Light Mode
    └── img/
        ├── indexbild.avif                 ← Titelbild auf der Startseite
        └── team/                          ← Porträtfotos der Ansprechpersonen (adrian, jeremy, nicolas, nils)
```

---

## Funktionen der Website

- **Startseite (`index.html`):** Einführung in den Club, Übersicht der vier Hauptbereiche (Über uns, Termine, Rangliste, Schach lernen) sowie direkter Link zur Anmeldung.
- **Über uns (`pages/ueber-uns.html`):** Vorstellung der Clubkultur (von Einsteigern bis Turnierspielern) und Ablauf der Trainingsabende.
- **Rangliste (`pages/rangliste.html`):** Umschaltbare Tabellen für **Schnellschach (10+5)** und **Blitz (3+2)** mit Platzierung, Trend, Studiengang, Elo-Rating, W-D-L-Bilanz und 5-Spiele-Form sowie einer Statistik-Sidebar (*DHBW-Spieler*, *Partien im Semester*, *Partien heute*, *Partien gerade*).
- **Termine (`pages/termine.html`):** Karten für konkrete Events (inkl. Turniere und DHBW-Standortvergleich) sowie Übersicht der regelmäßigen Treffen in der Theoriephase (Pause in der Praxisphase von Januar bis März).
- **Schach lernen (`pages/lernen.html`):** Interaktives 8×8-Schachbrett mit `a–h`/`1–8`-Koordinaten zum Auswählen der 6 Figuren inkl. Zugfeldern, Schlagzielen und einheitlichen Steckbriefen; 4-teiliges Regel-Karussell (Schachmatt/Patt, Rochade, Umwandlung/En passant, Eröffnungsregeln) sowie kuratierte externe Lernlinks.
- **Anmeldung & Kontakt (`pages/anmeldung.html`, `pages/kontakt.html`):** Aufklappbares FAQ, unverbindliche Schnupper-Bestätigung, Formular zur Club-/Turnieranmeldung (inkl. Spielstärke und Verteiler-Auswahl) sowie Teamkarten und Kontaktformular.
- **Rechtliches (`pages/impressum.html`, `pages/datenschutz.html`):** Transparente Kennzeichnung als fiktives Lehrprojekt inkl. Angaben zu GitHub Pages, lokalen Schriftarten und externen Links.

---

## Code- & CSS-Architektur

Alle HTML-Seiten binden ausschließlich `css/style.css` ein, die über `@import` vier spezialisierte Module lädt (`base.css` → `layout.css` → `components.css` → `pages.css`). Farben, Abstände und Schriften sind zentral über CSS Custom Properties in `css/base.css` definiert.

### Interaktivität komplett ohne JavaScript (0 % JS)

Sämtliche interaktiven Elemente sind ausschließlich mit nativem HTML5 und modernem CSS3 umgesetzt:

| Funktion | Technische Umsetzung | Datei |
|---|---|---|
| **Dark / Light Mode** | Übernimmt per `@media (prefers-color-scheme: light)` beim Laden den System-Standard; Umschalten über Checkbox `#theme-toggle` + `:root:has(#theme-toggle:checked)` inkl. Wechsel der `--theme-*`-Variablen und des Logos | `css/base.css`, `css/layout.css` |
| **Sprachwahl-Schalter** | Radio-Buttons `#lang-de` / `#lang-en` im Header; bei Auswahl von `English` blendet `:root:has(#lang-en:checked)` einen Hinweisbanner unter dem Header ein | `css/layout.css` |
| **Header-Menü** | Natives `<details class="site-menu">` und `<summary>` | alle HTML-Seiten, `css/layout.css` |
| **Schnellschach / Blitz** | Versteckte Radio-Buttons (`#modus-standard`, `#modus-blitz`) mit Geschwister-Selektoren (`~`) und fester `table-layout: fixed`-Spaltenbreite | `pages/rangliste.html`, `css/pages.css` |
| **Interaktives 8×8-Brett** | CSS Grid + 7 Radio-Buttons (`#figur-start` bis `#figur-bauer`); je nach ausgewählter Figur werden `.zug-punkt` und `.ziel-*` eingeblendet | `pages/lernen.html`, `css/pages.css` |
| **Regel-Karussell** | 4 Radio-Buttons (`#regel-1` bis `#regel-4`) mit Vor-/Zurück-Pfeilen als `<label>` | `pages/lernen.html`, `css/pages.css` |
| **FAQ-Akkordeon** | Natives `<details>` / `<summary>` | `pages/anmeldung.html` |
| **Formular-Bestätigung** | CSS `:target`-Pseudoklasse (`action="#anmeldung-bestaetigung"` bzw. `#kontakt-bestaetigung`) + Checkbox-Toggle für das Schnuppertraining | `pages/anmeldung.html`, `pages/kontakt.html` |

---

## Qualität, Barrierefreiheit & Datenschutz

- **Strikte JS-Freiheit:** Keine `<script>`-Tags, keine Inline-Event-Handler und keine externen JS-Bibliotheken.
- **Barrierefreiheit (WCAG 2.2 Level AA):**
  - Skip-Link (`Zum Inhalt springen` → `#inhalt`) auf jeder Seite.
  - Semantische HTML5-Landmarks (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`).
  - Sichtbare `:focus-visible`-Ringe für alle Links, Buttons, Checkboxen, Radio-Labels und Formularfelder.
  - Abgestimmte Kontrastwerte sowohl im Dark Mode als auch im Light Mode (z. B. angepasste Zugpunkt-Farben auf hellen/dunklen Brettfeldern).
  - Verknüpfte `<label for="...">` für alle Formularfelder sowie `aria-hidden="true"` bei dekorativen SVGs.
- **Responsive Design:** Flüssig bedienbar von **320 px bis 1920 px** (und bei > 200 % Browser-Zoom) ohne horizontales Scrollen; die Rangliste scrollt bei Bedarf sauber innerhalb von `.tabelle-scroll`.
- **Datenschutz & Unabhängigkeit:** Schriftart *Montserrat* (`400`, `600`, `700`) wird lokal aus `assets/fonts/` geladen – keine Anfragen an externe CDNs wie Google Fonts. Alle HTML-Seiten tragen `<meta name="robots" content="noindex, nofollow">`.

---

## Geplante Funktionen (Ausblick)

Für künftige Ausbaustufen (sobald Backend / JavaScript eingesetzt werden dürfen) sind folgende Erweiterungen vorgesehen:

1. **Automatisierte Rangliste & Live-Statistiken:** Anbindung an die Chess.com-API (oder ein eigenes Club-Backend), um aktuelle Elo-Werte, Partien und die Statistik-Sidebar (*Partien heute*, *Partien gerade*) dynamisch zu befüllen.
2. **Echte Formularverarbeitung:** Server-seitige Speicherung von Anmeldungen, Platzreservierungen für Raum A4.14 (max. 16 Bretter) sowie automatische Aufnahme in den E-Mail-/WhatsApp-Verteiler.
3. **Mehrsprachigkeit (Deutsch / Englisch):** Vollständige englische Sprachversion (z. B. über ein eigenes `/en/`-Verzeichnis oder dynamische Übersetzung über den bereits vorbereiteten Sprachschalter im Header).
4. **Echte Club-Fotografie:** Ersetzen der drei Bild-Platzhalter auf `pages/ueber-uns.html` durch eigene Fotos von Trainingsabenden und Turnieren.

---

## Medien & Hinweise

- **Startseitenbild (`assets/img/indexbild.avif`):** Quelle über [Unsplash (Schachpartie am Tisch)](https://unsplash.com/de/fotos/zwei-manner-die-an-einem-tisch-sitzen-und-eine-partie-schach-spielen-5V_AYHvt_Gw).
- **Pflicht-Hinweis:** Dies ist ein fiktives Studienprojekt im Rahmen der Webentwicklung-Vorlesung an der DHBW Heidenheim. Alle Ranglistenwerte, E-Mail-Adressen und Termine dienen ausschließlich zu Demonstrationszwecken.
