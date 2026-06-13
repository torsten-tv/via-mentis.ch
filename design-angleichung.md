# Website-Angleichung an den Flyer — Design-Vorschläge

**Stand:** 2026-06-12
**Ziel:** Einheitliches Markenbild zwischen dem A6-Flyer (`Flyer via-mentis/`) und der
Website (`via-mentis.html`, `ueber-uns.html`, `kontakt.html`). Der Flyer ist die Referenz.

---

## Ausgangslage (Ist) vs. Flyer (Soll)

| Element        | Website aktuell                              | Flyer (Soll)                                  |
|----------------|----------------------------------------------|-----------------------------------------------|
| Logo           | rundes Emblem `images/logo-neu.png`          | `logo-final.png` (VM-Wortmarke Oliv/Terracotta)|
| Headline-Font  | Cormorant Garamond                           | **Marcellus**                                 |
| Display/Labels | Raleway                                       | Marcellus (Großbuchstaben, weites Tracking)   |
| Body-Font      | Inter                                         | Inter (bleibt, nur Kleintext)                 |
| Grundfarbe     | Champagne `#f5e9d0` + Noise-Textur           | Salbei `#e3e6da`, clean                       |
| Primärfarbe    | Ink-Blau `#2d4668`                            | Anthrazit `#2a2a2a`                           |
| Akzent grün    | Sage `#5e7a64` / `#4d6852`                    | Oliv `#6f745e` / `#565b46`                    |
| Akzent warm    | Terracotta `#c89878` (blass)                  | **Terracotta `#c66f52`** (kräftiger, Logo-M)  |
| Buttons        | Sage-Grün-Verlauf                             | Oliv-Verlauf, Terracotta als Mikro-Akzent     |

Kernproblem: Website wirkt **warm-beige/blau**, Flyer wirkt **kühl-salbei/oliv mit
Terracotta-Akzent**. Andere Schrift, anderes Logo → aktuell nicht als eine Marke erkennbar.

---

## Vorschläge (priorisiert)

### 1. Logo vereinheitlichen  ★ höchste Wirkung
- Auf allen drei Seiten `images/logo-neu.png` durch das **finale Logo** ersetzen
  (`logo-final.png`, freigestellt als `logo-via-mentis.png` aus dem Flyer-Ordner übernehmen).
- Den separaten `<h1>Via Mentis</h1>`-Schriftzug auf der Startseite **entfernen** —
  das Wort „VIA MENTIS" steckt bereits im Logo (Doppelung vermeiden).
- `drop-shadow`-Filter dezenter / entfernen: der Flyer setzt das Logo flach und ruhig.

### 2. Typografie auf Marcellus umstellen
- Google-Fonts-Link ergänzen: `Marcellus` (+ ggf. `Marcellus SC` für Kapitälchen).
- Tailwind `fontFamily`: `serif/display → ['"Marcellus"','Georgia','serif']`,
  `sans → ['Inter','sans-serif']` (nur Body/Kleintext/Formular).
- Alle Headlines (`h1`, `h2`, Claim) auf Marcellus. Cormorant Garamond + Raleway entfernen.
- **Kein Kursiv** (Projektregel) — vorhandene `italic`-Klassen prüfen/entfernen.

### 3. Farbpalette austauschen (Tailwind-Config)
Neue Tokens (aus dem Flyer):
```js
colors: {
  ground:     '#e3e6da',  // Seiten-Hintergrund (Salbei)
  panel:      '#d6dac8',  // Karten/Boxen
  line:       '#c4c6b8',  // feine Linien/Rahmen
  olive:      '#6f745e',
  'olive-deep':'#565b46',
  terracotta: '#c66f52',  // Akzent (Logo-M), sparsam
  ink:        '#2a2a2a',  // Headlines
  text:       '#3f3f3b',  // Fließtext
  muted:      '#7a786f',  // Sekundärtext
}
```
- `bg-champagne` → `bg-ground`; `text-ink`/`ink-deep` (Blau) → neues `ink` (Anthrazit).
- Sage-Töne → Oliv-Töne. Blasses Terracotta → kräftiges `#c66f52`, aber **nur als Akzent**
  (Divider-Punkt, Pflichtstern, einzelne Linien) — nicht flächig.

### 4. Hintergrund & Textur beruhigen
- **Noise-Overlay (`body::before`) entfernen** oder Opacity auf ~0.05 senken — der Flyer ist clean.
- Optional auf Unterseiten ein **dünner Oliv-Rahmen** (`border border-line`) als Echo des
  Flyer-Rahmens, mit großzügigem Innenabstand.

### 5. Komponenten anpassen
- **Buttons/CTA:** Verlauf von Oliv `#6f745e → #565b46` statt Sage-Grün; Hover etwas heller.
  Alternativ ruhiger: Anthrazit-Fläche mit Terracotta-Hover-Linie.
- **Divider** (Linie·Punkt·Linie): Linien in `line`/Oliv, Punkt in **Terracotta** — exakt wie Flyer-Rückseite.
- **Karten/Formular:** Hintergrund `panel`, Rand `line`; weichere, flachere Schatten (weniger „Glas/Blur").
- **Angebot-Liste** (von der Flyer-Rückseite übernehmen): Blöcke mit linkem Oliv-Akzentstrich
  + `·`-Bullets — schafft direkte Wiedererkennung zum Flyer.
- **Eyebrows/Labels:** Marcellus, Großbuchstaben, weites Tracking (`tracking-[0.16em]`), Farbe `olive-deep`.

### 6. Inhaltliche Brücken zum Flyer
- Claim der Startseite an den Flyer angleichen: „Unterstützung, wenn das Leben herausfordernd
  wird. Psychosoziale Begleitung im Alltag."
- Angebots-Dreiteilung (Alltag & Struktur · Psychische Gesundheit · Vernetzung & Begleitung)
  und „Für wen?"-Box 1:1 als Website-Sektionen übernehmen.

---

## Empfohlene Umsetzungsreihenfolge
1. Tailwind-Farb-Config + `bg-ground` global (sofort sichtbarer Effekt).
2. Marcellus einbinden + Headlines umstellen.
3. Logo tauschen + doppelten Schriftzug entfernen.
4. Noise/Schatten beruhigen, Divider/Buttons recolorieren.
5. Angebot-Sektion + „Für wen?"-Box vom Flyer übernehmen.
6. Feinschliff: Abstände, Rahmen-Echo, Kontrolle „kein Kursiv".

> Hinweis: Tailwind bleibt für die Website Pflicht. Vor Umsetzung gerne 1–2 Seiten als
> Vorschau, bevor alle drei Seiten umgestellt werden.
