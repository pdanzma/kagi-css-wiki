# Kagi Custom CSS Wiki

Ein umfassender Leitfaden für die Entwicklung eigener Custom CSS Themes für die Kagi Suchmaschine. 

## Inhaltsverzeichnis

1. [Erste Schritte](#erste-schritte)
2. [Kagi DOM-Struktur verstehen](#kagi-dom-struktur-verstehen)
3. [CSS-Variablen und Theming](#css-variablen-und-theming)
4. [Wichtige CSS-Selektoren](#wichtige-css-selektoren)
5. [Animationen und Hover-Effekte](#animationen-und-hover-effekte)
6. [Community-Projekte analysieren](#community-projekte-analysieren)
7. [Tipps & Tricks](#tipps--tricks)
8. [Häufige Probleme & Lösungen](#häufige-probleme--lösungen)
9. [Ressourcen & Links](#ressourcen--links)

---

## Erste Schritte

### Installation und Aktivierung

1. **CSS-Editor erreichen**: Gehe zu den [Kagi Einstellungen](https://kagi.com/settings?p=custom_css)
2. **Custom CSS aktivieren**: Schalte den Toggle "Benutzerdefiniertes CSS aktivieren" ein
3. **CSS eingeben**: Füge den CSS-Code in das Textfeld ein (max. 40.000 Zeichen - Stand August 2025)
4. **Testen**: Verwende `kagi.com/search?q=test&no_css` zum Deaktivieren der CSS Datei bei Problemen

### Grundlegende Template-Struktur

Das ist üblich, um sich selbst in dem Projekt zu erwähnen und Lizenzprobleme zu vermeiden. Das :root-Element ändert alles im Dokument. Die Farbe wird im HEX-Format angegeben, also zum Beispiel #FFFFFF für Weiß. Die Groß- und Kleinschreibung ist egal. Es kann auch #ffffff heißen.

Auffallend ist auch die Funktion zum Hinterlegen von Kommentaren. Das passiert mit ```/* ... */ ```. Bitte beachte: Auch die Kommentare werden als Zeichen gewertet und sollten nach Möglichkeit minimiert oder entfernt werden, wenn man später an die Obergrenze für Zeichen gelangt.

```css
/* ===========================================
   KAGI CUSTOM CSS THEME
   Autor: [Dein Name]
   Version: 1.0
   =========================================== */

/* CSS-Variablen definieren */
:root {
  --primary-color: #your-color; /*  */
  --secondary-color: #your-color;
  --background-color: #your-color;
  --text-color: #your-color;
}

/* Dark Mode Variablen */
.theme_dark,
.theme_moon_dark {
  --primary-color: #your-dark-color;
  /* weitere Dark Mode Farben */
}

/* Responsive Design */
@media (max-width: 768px) {
  /* Mobile Anpassungen */
}
```

### Einsatz des Inspectors

Der Inspector ist ein Entwicklerwerkzeug, mit dem man die Struktur und Gestaltung von Webseiten analysieren und bearbeiten kann. Er ermöglicht es, HTML-Elemente, CSS-Stile und das Layout direkt im Browser zu untersuchen und zu verändern. 

Hilfsseite zum Einstieg von Microsoft Learn: [Microsoft Learn Inspector Tool](https://learn.microsoft.com/de-de/microsoft-edge/devtools/css/inspect)

### Nutzung des Inspectors in Firefox
- Suche bspw. 'test' in der Kagi Suche
- Klicke mit der **rechten Maustaste** auf das Element, welches inspeziert werden soll. 
- Wähle im Kontextmenü die Option 'Element untersuchen' (unterscheidet sich von Browser zu Browser)
- Alternativ kann man den Inspector auch über die Tastenkombination **F12** oder **Strg+Shift+I** (Windows/Linux) bzw. **Cmd+Option+I** (Mac) öffnen.
- Der Inspector erscheint in einem Bereich am unteren oder seitlichen Rand des Browserfensters, wo der HTML-Quellcode und die dazugehörigen CSS-Stile angeschaut und bearbeitet werden kann.

### Nutzung des Inspectors in Chrome
- Suche bspw. 'test' in der Kagi Suche
- Klicke mit der **rechten Maustaste** auf das Element, welches inspeziert werden soll. 
- Wähle im Kontextmenü die Option 'Untersuchen' (unterscheidet sich von Browser zu Browser)
- Alternativ kann man den Inspector auch über die Tastenkombination **F12** oder **Strg+Shift+I** (Windows/Linux) bzw. **Cmd+Option+I** (Mac) öffnen.
- Der Inspector erscheint in einem Bereich am unteren oder seitlichen Rand des Browserfensters, wo der HTML-Quellcode und die dazugehörigen CSS-Stile angeschaut und bearbeitet werden kann.

---

## Kagi DOM-Struktur verstehen

Die HTML- und CSS-Struktur ist in einer sogenannten DOM-Struktur aufgebaut. Bitte beachte, dass verschiedene Elemente voneinander abhängig sind. Dies ist bei der Bearbeitung zu berücksichtigen. Beispiel hierfür:

```css
.d-info-box-title-header.--trackers
```

### Haupt-Container

```css
/* Hauptlayout-Container */
.app-header          /* Kopfzeile mit Suchleiste */
.app-content         /* Hauptinhalt */
.center-content-box  /* Zentrale Inhaltsbox */
.right-content-box   /* Rechte Sidebar (Wikipedia, etc.) */
.search-form         /* Suchformular */
.search-results      /* Suchergebnisse Container */
```

### Suchergebnisse

```css
/* Suchergebnis-Elemente */
.search-result       /* Einzelnes Suchergebnis */
.__sri-title         /* Ergebnis-Titel */
.__sri-url           /* URL-Anzeige */
.__sri-desc          /* Beschreibungstext */
.__sri-time          /* Zeitstempel */

/* Gruppierte Ergebnisse */
.sri-group           /* Gruppierte Suchergebnisse */
.__srgi              /* Einzelelement in Gruppe */
```

### Navigation und Filter

```css
/* Navigation */
.serp-nav           /* Hauptnavigation (Web, Bilder, Videos, etc.) */
.nav_item           /* Navigationselemente */
.sidebar-filter-nav-form /* Filter-Navigation */

/* Lenses (Suchfilter) */
._0_lenses          /* Lenses Container */
.k_ui_dropdown      /* Dropdown-Menüs */
```

---

## CSS-Variablen und Theming

### Wichtige Kagi CSS-Variablen

```css
:root {
  /* Grundfarben */
  --app-bg: #ffffff;                    /* Haupthintergrund */
  --app-text: #000000;                  /* Haupttext */
  --primary: #18181a;                   /* Primärfarbe */
  --secondary: #ffffff;                 /* Sekundärfarbe */
  
  /* Such-Interface */
  --color-search-input: #ffffff;        /* Suchfeld Hintergrund */
  --color-search-input-border: #e6e6e8; /* Suchfeld Rahmen */
  
  /* Suchergebnisse */
  --search-result-title: #18181a;       /* Titel-Farbe */
  --search-result-content-text: #5a5a60; /* Beschreibungstext */
  --search-result-url-link: #707077;    /* URL-Farbe */
  
  /* Hover-Effekte */
  --hover-bg: rgba(172, 172, 175, 0.1); /* Hover-Hintergrund */
  --primary-hover: #6c5edc;             /* Hover-Farbe */
  
  /* Abstände */
  --search-result-gap: 32px;            /* Abstand zwischen Ergebnissen */
}
```

### Dark Mode Anpassungen

```css
.theme_dark,
.theme_moon_dark {
  --app-bg: #22242f;
  --app-text: #ffffff;
  --primary: #ffffff;
  --secondary: #22242f;
  
  /* Such-Interface für Dark Mode */
  --color-search-input: #2f2f31;
  --color-search-input-border: #454549;
  
  /* Angepasste Farben für bessere Lesbarkeit */
  --search-result-title: #ffffff;
  --search-result-content-text: #cfcfdb;
}
```

### Eigene Variablen definieren

```css
:root {
  /* Deine eigenen Variablen */
  --brand-primary: #ff6b35;
  --brand-secondary: #004e89;
  --brand-accent: #f7931e;
  
  /* Größen */
  --border-radius: 8px;
  --box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  
  /* Animationen */
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
}
```

---

## Wichtige CSS-Selektoren

### Suchleiste anpassen

```css
/* Suchformular */
.search-form {
  /* Deine Styles */
}

/* Suchfeld */
.search-input {
  background: var(--color-search-input);
  border: 1px solid var(--color-search-input-border);
  border-radius: var(--border-radius);
  transition: var(--transition-normal);
}

/* Suchfeld fokussiert */
.search-input:focus {
  border-color: var(--brand-primary);
  box-shadow: 0 0 0 3px rgba(255, 107, 53, 0.1);
}
```

### Suchergebnisse stylen

```css
/* Suchergebnis Container */
.search-result {
  padding: 20px;
  margin-bottom: var(--search-result-gap);
  border-radius: var(--border-radius);
  transition: var(--transition-normal);
}

/* Hover-Effekt für Suchergebnisse */
.search-result:hover {
  background-color: var(--hover-bg);
  transform: translateY(-2px);
  box-shadow: var(--box-shadow);
}

/* Titel-Links */
.__sri-title .__sri_title_link {
  color: var(--brand-primary);
  text-decoration: none;
  border-bottom: 2px solid transparent;
  transition: var(--transition-fast);
}

.__sri-title .__sri_title_link:hover {
  border-bottom-color: var(--brand-primary);
}
```

### Navigation anpassen

```css
/* Hauptnavigation */
.serp-nav {
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border-radius: var(--border-radius);
  padding: 10px;
}

/* Navigationsitems */
.serp-nav .nav_item {
  padding: 8px 16px;
  border-radius: calc(var(--border-radius) / 2);
  transition: var(--transition-fast);
}

.serp-nav .nav_item:hover,
.serp-nav .nav_item.--active {
  background-color: var(--brand-primary);
  color: white;
}
```

### Font ändern

Auch wenn dies nicht die bevorzugte Vorgehensweise des Kagi Staff ist (ein kleiner Scherz am Rande), besteht die Möglichkeit, die globale Schriftart mittels CSS zu ändern. Standardmäßig ist die Schriftart "Lufga" eingestellt, die mithilfe der folgenden Regel an die gewünschte Schriftart angepasst werden kann.

```css
/* Ändert die Font zu Arial */
body {
    font-family: Arial, sans-serif !important;
}
```

---

## Animationen und Hover-Effekte

In dieser Sektion werden verschiedene Animationsarten behandelt, die ausschließlich mit CSS realisiert werden könenn. Hover-Effekte für diverse Buttons sind in der Regel einfach zu realisieren und ausreichend. Für die Einbindung von tiefen und komplexeren Animationen empfiehlt sich die Beispielimplementierung einer Fade-In-Animation anzuschauen, die die Suchergebnisse langsam einblendet. Es sollte jedoch beachtet werden, dass zu viele oder zu lange Animationen als störend empfunden werden und die Benutzererfahrung beeinträchtigen können. Darüber hinaus ist es empfehlenswert, bei Animationen einen Reduced-Motion-Modus zu implementieren. Dies ermöglicht es den Nutzern, die keine Animationen wünschen, diese in ihren Browsereinstellungen zu deaktivieren.

### Fade-In Animation für Suchergebnisse

```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.search-result {
  animation: fadeInUp 0.3s ease forwards;
}

/* Gestaffelte Animation */
.search-result:nth-child(1) { animation-delay: 0.1s; }
.search-result:nth-child(2) { animation-delay: 0.2s; }
.search-result:nth-child(3) { animation-delay: 0.3s; }
/* usw. */
```

### Hover-Effekte für Buttons

```css
.k_ui_btn_group .k_ui_btn {
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease;
}

.k_ui_btn_group .k_ui_btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.k_ui_btn_group .k_ui_btn:hover::before {
  left: 100%;
}
```

### Glassmorphism-Effekt

Gerne möchte ich Ihnen einen kleinen Exkurs zu meinem eigenen Thema geben. Diese Richtlinien implementieren einen Milchglas-Effekt für verschiedene Elemente, der ein Alleinstellungsmerkmal meines Themes ist. Sollten Sie diese Funktion auch gerne in Ihrem Theme haben wollen, beispielsweise als Theme in Anlehnung des Liquid Glass Themes von Apple, können Sie diese Regel gerne übernehmen und in Ihr Theme einbauen. Ich empfehle Ihnen außerdem die Seite [css glass](https://css.glass), auf der Sie benutzerdefinierte Glasseffekte generieren lassen können.

```css
.glassmorphism {
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: var(--border-radius);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
}
```

### Reduced Motion Property

Wenn der Benutzer im Browser diesen Modus eingestellt hat, sollten wir als CSS-Designer das respektieren und optimal umsetzen. Bitte überprüfen Sie Ihre implementierten Animationen und setzen Sie sie unter diesem Property explizit auf "none". Dies führt zu einer signifikanten Steigerung der Benutzerfreundlichkeit.

```css
  /* Reduced Motion Override*/
  @media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
      animation-duration: 0.001ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.001ms !important;
      scroll-behavior: auto !important;
    }
    
    /* Hier explizit, wenn die Fade In Animation verwendet wird */
    .sri-group {
      opacity: 1;
      transform: none;
      animation: none;
    }
    
    /* Ersetzt komplexe Animationen durch einfache Fade (nur wenn man eine Background-Animation implementiert hat) */
    @keyframes moveBackground {
      to { transform: translate(0, 0); }
    }
  }
  
  /* Respektiere auch no-preference explizit */
  @media (prefers-reduced-motion: no-preference) {
    .enhanced-animation {
      animation: complexMove 2s ease-in-out infinite;
    }
  }
```

### Pseudoelemente

Im CSS-Design von Projekten wie **korp-net** spielen Pseudoelemente eine zentrale Rolle, um visuelle Effekte und dekorative Elemente elegant und performant darzustellen, ohne zusätzliche HTML-Strukturen im DOM hinzufügen zu müssen - was eh nicht möglich ist.

```css
/* Ziemlich komplex, aber falls die Beschreibung einer Webseite leer ist, kommt dieser Text als Pseudoelement */
.__sri-desc:has(>div:empty)::before {
    content: "// DESCRIPTION REDACTED_OR_UNAVAILABLE //";
}
```

### Zählervariable

Eine weitere Option, um Ihrem Design eine gewisse Einzigartigkeit zu verleihen, sind Zählvariablen. Diese sind im Codebeispiel für die Zählung der einzelnen Suchergebnisse ersichtlich.

```css
._0_main-search-results {
    counter-reset: result-counter
}

.search-result>._0_TITLE::before {
    counter-increment: result-counter;
    content: "PACKET_ID: 0" counter(result-counter)" // STATUS: [COMPLETE]";
}
```

---

## Community-Projekte analysieren

Eine effektive Methode, um nach geeigneten Properties zu suchen, ist die Analyse bereits bestehender Community-Projekte. Für diesen Zweck eignen sich alle bereits veröffentlichten Projekte. Nachfolgend finden Sie einige Beispiele:

### [Kagi-CSS von pdanzma](https://github.com/pdanzma/kagi-css)

**Highlights:**
- Glassmorphism-Design
- Einfache Farbkonfiguration über CSS-Variablen
- Responsive Design

### [Kagi-Darker von realrogue](https://github.com/realrogue/kagi-darker)

**Highlights:**
- Pure schwarze Hintergründe optimal für OLED-Displays
- Glassmorphism-Header auf Desktop
- Bubble-Design für Kagi Assistant
- Mobile-optimiert

**Lernpunkte:**
- Benutzer-konfigurierbare Farben am Anfang der CSS-Datei
- Klare Trennung von Desktop- und Mobile-Styles
- Fokus auf Zugänglichkeit


### [Liquid Glass Theme von 0xGingi](https://github.com/0xGingi/kagi-liquid-glass-theme)

**Highlights:**
- Implementiert das Liquid Glass Theme von Apple
- Gute Dokumentation

### [Catppuchin Theme von jcrabapple](https://github.com/jcrabapple/kagi-catppuccin-light-dark)

**Highlights:**
- Sehr gute Dokumentation
- Automatischer Wechsel zwischen Hellem und Dunklem-Theme


### [Korp Net Theme von pdanzma](https://github.com/pdanzma/korp-net)

**Highlights:**
- Kompletter Overhaul des bestehenden Designs
- Suchleiste unten, falls es auch in dein Theme soll

Grundsätzlich ist anzumerken, dass nahezu alle Community-Themes auch geforkt werden können. Dies ist eine Option, wenn ein bestehendes Theme nach den individuellen Wünschen angepasst und anschließend der Community zur Verfügung gestellt werden soll.
---

## Tipps & Tricks

### 1. Debugging und Entwicklung

```css
/* Debug-Modus: Zeige alle Container-Grenzen */
.debug * {
  outline: 1px solid red !important;
}

/* Temporär zum Body hinzufügen */
body.debug * {
  outline: 1px solid rgba(255, 0, 0, 0.3) !important;
}
```

### 2. CSS-Variablen effektiv nutzen

```css
/* Schlecht: Werte mehrmals wiederholen */
.element1 { color: #ff6b35; }
.element2 { border-color: #ff6b35; }
.element3 { background: #ff6b35; }

/* Gut: Variable verwenden */
:root { --brand-color: #ff6b35; }
.element1 { color: var(--brand-color); }
.element2 { border-color: var(--brand-color); }
.element3 { background: var(--brand-color); }
```

### 3. Responsive Design

```css
/* Mobile First Approach */
.search-result {
  padding: 10px;
  font-size: 14px;
}

/* Tablet */
@media (min-width: 768px) {
  .search-result {
    padding: 15px;
    font-size: 16px;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .search-result {
    padding: 20px;
    font-size: 18px;
  }
}
```

### 4. Performance-Optimierung

```css
/* Animationen auf GPU verlagern */
.animated-element {
  transform: translateZ(0); /* GPU-Beschleunigung erzwingen */
  will-change: transform;   /* Hint für Browser */
}

/* Animationen nur bei Hover */
@media (hover: hover) {
  .hover-effect:hover {
    transform: translateY(-2px);
  }
}
```

### 5. Browser-Kompatibilität

Hier ist zu beachten, dass nicht alle neueren CSS-Regeln von allen Browsern unterstützt werden. Für dieses Vorhaben besteht die Möglichkeit, einen Fallback für ältere Browser zu implementieren, sodass auch Browser ohne Kompatibilität für neuere Regeln das Custom CSS benutzen können.

```css
/* Fallbacks für ältere Browser */
.modern-gradient {
  background: #ff6b35; /* Fallback */
  background: linear-gradient(135deg, #ff6b35 0%, #004e89 100%);
}

/* Unterstützung prüfen */
@supports (backdrop-filter: blur(10px)) {
  .glassmorphism {
    backdrop-filter: blur(10px);
  }
}
```

---

## Häufige Probleme & Lösungen

### Problem: Styles werden nicht angewendet

**Ursachen & Lösungen:**

1. **Spezifität zu niedrig**
   ```css
   /* Schwach */
   .button { color: red; }
   
   /* Stärker */
   .search-form .button { color: red; }
   
   /* Stärkste (nur wenn nötig, die !important ist sehr stark und überschreibt andere Regeln) */
   .search-form .button { color: red !important; }
   ```

2. **Falsche Selektoren**
   ```css
   /* Falsch */
   .search_result { }
   
   /* Richtig */
   .search-result { }
   ```

### Problem: Animationen ruckeln

**Lösungen:**
```css
/* GPU-Beschleunigung aktivieren */
.smooth-animation {
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000;
}

/* Nur transform und opacity animieren */
.performance-animation {
  transition: transform 0.3s ease, opacity 0.3s ease;
}
```

### Problem: Mobile Darstellung

**Lösungen:**
```css
/* Touch-freundliche Größen */
.mobile-friendly {
  min-height: 44px; /* Mindest-Touch-Target */
  padding: 12px;
}

/* Viewport-spezifische Einheiten */
.full-width {
  width: 100vw;
  margin-left: calc(50% - 50vw);
}
```

---

## Ressourcen & Links

### Offizielle Kagi-Ressourcen

- [Kagi Custom CSS Dokumentation](https://help.kagi.com/kagi/features/custom-css.html)
- [Kagi Appearance Settings](https://help.kagi.com/kagi/settings/appearance.html)
- [Community Themes Collection](https://github.com/kawaiier/awesome-kagi-css)

### CSS-Lernressourcen

- [CSS-Tricks Complete Guide to CSS](https://css-tricks.com/guides/)
- [MDN CSS Reference](https://developer.mozilla.org/de/docs/Web/CSS)
- [CSS Selectors Cheat Sheet](https://www.freecodecamp.org/news/css-selectors-cheat-sheet-for-beginners/)

### Tools und Hilfsmittel

- [CSS Compressor](https://css.github.io/csso/csso.html)
- [Glassmorphism Generator](https://glassmorphism.com/)
- [CSS Animation Generator](https://animista.net/)
- [Color Palette Tools](https://coolors.co/)

### Community

- [Kagi Discord](https://discord.gg/kagi) - verschiedene Channel für Design
- [r/SearchKagi Subreddit](https://www.reddit.com/r/SearchKagi/)
- [r/KagiUserCSS Subreddit](https://www.reddit.com/r/KagiUserCSS/)

### Neueste CSS-Features (2024/2025)

- **Container Queries**: Responsive Design basierend auf Container-Größe
- **:has() Pseudo-Klasse**: Parent-Selektoren in CSS
- **CSS Nesting**: Native Verschachtelung ohne Preprocessor
- **CSS Cascade Layers**: Bessere Kontrolle über Spezifität
- **New Color Functions**: `lch()`, `lab()`, `hwb()`

### Code-Beispiele für moderne CSS-Features

```css
/* Container Queries */
@container (min-width: 300px) {
  .search-result {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}

/* :has() Pseudo-Klasse */
.search-result:has(.sri-time) {
  background-color: var(--highlight-bg);
}

/* CSS Nesting */
.search-form {
  background: white;
  
  .search-input {
    border: none;
    
    &:focus {
      outline: 2px solid var(--brand-primary);
    }
  }
}

/* Cascade Layers */
@layer base, theme, utilities;

@layer base {
  .search-result { color: black; }
}

@layer theme {
  .search-result { color: var(--text-color); }
}
```

---

## Mitwirken

Dieses Wiki ist ein Community-Projekt. Contributions sind willkommen!

### Wie du beitragen kannst:

1. **Neue Selektoren dokumentieren** - Wenn du neue Kagi-CSS-Klassen findest
2. **Beispiele hinzufügen** - Teile deine CSS-Tricks
3. **Bugs melden** - Wenn etwas nicht funktioniert
4. **Verbesserungen vorschlagen** - Für bessere Erklärungen

### Template für neue Beiträge:

```markdown
### [Feature Name]

**Beschreibung:** Was macht dieses Feature?

**CSS-Selektor:** `.example-selector`

**Beispiel:**
```css
.example-selector {
  /* Dein Code hier */
}
```

**Browser-Support:** Chrome 90+, Firefox 88+, Safari 14+

---

*Letztes Update: August 2025*
*Version: 1.0*