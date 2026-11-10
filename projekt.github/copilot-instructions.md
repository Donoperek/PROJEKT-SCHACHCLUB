# GitHub Copilot Instructions: DHBW Schachportal

Diese Datei enthält die verbindlichen Arbeitsrichtlinien für GitHub Copilot bei der Unterstützung der Entwicklung des DHBW-Schachportals (Vorlesung Webentwicklung an der DHBW Heidenheim, Dozent: Jens Reiner).

---

## 1. Rolle & Arbeitsmodus bei Code-Prompts

* **Arbeitsweise**: Generiere **nur genau den Code oder die Komponente, die im Prompt angefordert wird** (z. B. ein einzelner Hero-Bereich, eine Tabelle für die Rangliste, ein Navigations-Header oder CSS-Regeln). Erstelle niemals unaufgefordert ganze Seitenbäume oder das Gesamtprojekt auf einmal.
* **Präzision**: Liefere sauberen, modularen, menschlich lesbaren und direkt integrierbaren HTML5- und CSS-Code.
* **Keine Annahmen**: Nutze für bestehende Klassen, Farbvariablen und Typografie die definierten Design-Tokens des Projekts.

* **Klare Dokumentation**: Kommentiere den Code, um die Funktionalität und Struktur zu erklären. Vermeide unnötige Kommentare, die den Code unübersichtlich machen.

---

## 2. Projekt-Kontext & Zielgruppe

* **Projekt**: Webplattform für die Schach-Community der DHBW Heidenheim.
* **Kernfunktionen**:
  * Organisation von Schachtrainings für Studierende im Anschluss an Vorlesungen.
  * Campus-Turniere (Blitz/Schnellschach) und Verwaltung der DHBW-Elo-Rangliste.
  * Vernetzung von Studierenden verschiedener Studiengänge.
  * Ausblick auf künftige interaktive Online-Schachfunktionen (Simulation über reines HTML/CSS).
* **Zielgruppe (ICP)**: Studierende der DHBW (18–26 Jahre), analytisch und technikaffin.
* **Tonalität**: Motivierend, schachspezifisch, kollegial („Du“-Form).
* **Inhaltlicher Standard**: **Kein „Lorem Ipsum“ oder beliebiger Fülltext!** Verwende stets schachspezifischen, plausiblen Text (z. B. „Sizilianische Verteidigung“, „Schweizer System“, „Elo 1420“, „Hörsaal 214“).

---

## 3. Strikte Hard-Constraints bei JEDER Code-Generierung

Die folgenden Regeln sind absolute Nicht-Verhandelbarkeiten aus den Vorgaben des Dozenten. Verstöße führen zu direktem Punktabzug:

### A. Striktes JavaScript-Verbot (0% Toleranz)
* **Kein `<script>`-Tag**, keine externen JS-Dateien, keine Frameworks (React, Vue etc.).
* **Keine Inline-Event-Handler** (`onclick`, `onchange`, `onload` etc.).
* **Keine `javascript:`-Pseudo-Protokolle** in Links.
* Wenn eine Interaktivität benötigt wird, **muss** diese mit reinem HTML5 und CSS gelöst werden.

### B. Barrierefreiheit (WCAG 2.2 Level AA)
* **Kontraste**: Fließtext mindestens `4.5:1`, Großtext/Icons mindestens `3.0:1`.
* **Tastaturbedienbarkeit**: Alle interaktiven Elemente müssen über `Tab` erreichbar sein. Niemals `outline: none` setzen, ohne einen deutlichen `:focus-visible`-Zustand zu definieren.
* **Semantik**: Verwende strikt semantische Tags (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`). Keine `<div>`-Wüsten.
* **Formulare**: Jedes Eingabefeld (`input`, `select`, `textarea`) besitzt ein verknüpftes `<label for="...">`.
* **Bilder**: Jedes `<img>` benötigt ein sinnvolles deutsches `alt`-Attribut (oder `alt=""` mit `aria-hidden="true"` bei reiner Dekoration).
* **Linktexte**: Niemals vage Bezeichnungen wie „hier klicken“ oder „mehr erfahren“. Verwende sprechende Links wie „Trainingszeiten ansehen“ oder „Zur Turnieranmeldung“.

### C. CSS & Styling
* Reines, modernes CSS mit **CSS Custom Properties** (Variablen).
* **Mobile-First Responsive Design**: Das Layout muss flüssig von **320px bis 1920px** ohne horizontales Scrollen funktionieren.
* Bevorzuge CSS Grid und Flexbox für alle Layouts.
* Keine externen CDN-Stylesheets, die Abhängigkeiten erzeugen.

---

## 4. Erlaubte Patterns für CSS-Only Interaktionen

Wenn der Nutzer interaktive Komponenten anfordert, setze ausschließlich diese Techniken ein:

1. **Akkordeons / Klappmenüs**: `<details>` und `<summary>` mit CSS-Styling.
2. **Modals / Overlays**: Über CSS `:target` (z. B. `<a href="#modal-id">` öffnet, `<a href="#">` schließt).
3. **Tabs / Umschalter**: Über den Hidden-Checkbox/Radio-Hack (`input[type="radio"]:checked + label + .tab-content`).
4. **Schachbrett-Visualisierung**: CSS Grid (8x8) mit semantischen Buttons/Feldern und Unicode-Schachsymbolen (`&#9812;` bis `&#9823;`) mit `aria-label`.

---

## 5. Design Tokens (Referenz für CSS)

Verwende bei Styles stets folgende Variablen als Basis:

```css
  farben bestimmt der nutzer 
  /* Typografie & Abstände */
  root {
  --font-main: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --radius-sm: 4px;
  --radius-md: 8px;
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}
```

---

## 6. Endprodukt-Prüfung & Audit-Modus (Quality Gate)

Wenn der Nutzer dich auffordert: **„Prüfe meinen Code“**, **„Führe ein Audit durch“** oder **„Entspricht das Projekt den Prüfungskriterien?“**, teste das Projekt anhand dieser Checkliste:

1. **JavaScript-Freiheit**: Enthält irgendeine Datei `<script>`, Inline-JS oder JS-Bibliotheken?
2. **Umfangskontrolle (Projektvorgabe)**:
   * Sind mindestens **8 HTML-Seiten** vorhanden?
   * Gibt es mindestens **4 unterschiedliche Seitenlayouts**?
3. **WCAG 2.2 AA Konformität**:
   * Sind Farbkontraste ausreichend?
   * Sind Focus-Ringe sichtbar vorhanden?
   * Haben alle Formularfelder zugehörige Labels?
   * Sind Alt-Texte und Skip-Links (`#main-content`) vorhanden?
4. **Integrität**:
   * Gibt es tote Links (`href="#"` ohne existierenden Anker)?
   * Laden alle lokalen Bilder korrekt (keine externen instabilen URLs)?
5. **Pflicht-Hinweis**:
   * Ist im Footer jeder Seite der Hinweis enthalten:
     *„Hinweis: Dies ist ein fiktives Studienprojekt im Rahmen der Webentwicklung-Vorlesung an der DHBW Heidenheim.“*
6. **Performance / Bahn-Test**:
   * Werden Bilder in maßvollen Auflösungen und modernen Formaten (WebP/SVG) geladen?