# Ayça Feza & Buğrahan — Kız İsteme & Nişan

Digitale Einladung zur türkisch-deutschen Verlobungsfeier.
Samstag, 27. Juni 2026 · Amselweg 10, 40878 Ratingen.

Eine einzelne `index.html` (HTML + CSS + JS inline) plus SVG-Illustration und Paar-Foto. Keine Frameworks, kein Build, reines Static Hosting.

---

## 1. Lokal öffnen

Einfach `index.html` doppelklicken – öffnet im Browser.

Falls das Foto oder die SVG nicht geladen wird (manche Browser blockieren `file://`-Zugriffe), lokal einen Mini-Server starten:

```bash
# aus dem Projektordner
python3 -m http.server 8000
# dann im Browser: http://localhost:8000
```

Oder mit Node:
```bash
npx serve .
```

---

## 2. Auf GitHub Pages deployen

1. Neues GitHub-Repo anlegen (z.B. `ayca-bugrahan-davet`) und den Projektordner reinpushen:
   ```bash
   git init
   git add .
   git commit -m "Einladung live"
   git branch -M main
   git remote add origin https://github.com/<USERNAME>/<REPO>.git
   git push -u origin main
   ```
2. Im Repo: **Settings → Pages**
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` · Folder: `/ (root)` → Save
3. Nach ~1 Min ist die Seite unter `https://<USERNAME>.github.io/<REPO>/` online.

### Eigene Domain (optional)
- Bei DNS-Provider einen `CNAME`-Eintrag auf `<USERNAME>.github.io` legen (bzw. vier A-Records auf die GitHub-Pages-IPs für Apex-Domains).
- Im Repo-Root eine Datei `CNAME` mit nur der Domain drin (eine Zeile, z.B. `davet.buayca.de`) committen.
- In **Settings → Pages** die Custom Domain eintragen und **Enforce HTTPS** aktivieren.

---

## 3. Texte & Daten anpassen

Alles liegt in `index.html`. Die wichtigsten Stellen:

| Was                       | Wo in `index.html`                                    |
| ------------------------- | ----------------------------------------------------- |
| Event-Datum / Uhrzeit / Dauer (Countdown **und** ICS) | `const EVENT = { … }` im `<script>`-Block — `startUTC` / `endUTC` anpassen. **Wichtig**: Zeiten in UTC angeben (Europe/Berlin im Juni = UTC+2, im Winter UTC+1). |
| ICS-Titel & Beschreibung  | `EVENT.titleTR`, `EVENT.titleDE`, `EVENT.descTR`, `EVENT.descDE` |
| ICS-Adresse               | `EVENT.location`                                      |
| Alle Texte (TR + DE)      | `const i18n = { tr: {…}, de: {…} }` — pro Sprache ein Objekt mit allen Strings |
| Namen im Hero             | `<h1 class="names">` (sind hart-codiert, keine Übersetzung nötig) |
| Google-Maps-Button-Link   | `<a class="action-btn" href="https://www.google.com/maps/search/?api=1&query=…">` in der Details-Section |
| Turkisches Zitat          | `<p class="quote-orig">` — bleibt in beiden Sprachen Türkisch |
| Übersetzung des Zitats    | `quoteTrans` im `i18n`-Objekt (TR: Paraphrase / DE: Übersetzung) |
| Paar-Foto                 | Datei `couple.jpeg` im Root durch eigenes ersetzen (Name gleich lassen oder im `<img src="…">` anpassen) |
| Hero-Video (Desktop)      | `assets/courtyard.mp4` — 16:9 Landscape, wird auf Viewports > 640px geladen. Umbenennen nur wenn `data-src-desktop="…"` im `<video>`-Element angepasst wird. |
| Hero-Video (Mobile)       | `assets/courtyard-mobile.mp4` — 9:16 Portrait, wird auf Viewports ≤ 640px geladen. Auswahl passiert über ein kleines Inline-Skript direkt nach dem `<video>`-Element. |
| Fallback-Illustration     | `assets/illustration.svg` — wird als Poster/Notbild angezeigt, wenn das Video nicht geladen werden kann |
| Schwebende Blütenblätter  | Im `<div class="petals">` direkt nach `<body>`: einzelne `.petal` entfernen → weniger; duplizieren + `p11` Klasse + Animation-Delay → mehr |
| Section-Dekorationen      | SVGs mit Klasse `section-deco` in jeder Section (Girlande, Zweige, Blüten). Einfach entfernen oder anpassen. |
| Farbpalette               | CSS-Variablen unter `:root { … }` (z.B. `--ink`, `--terra`, `--bg` …) |

### Standardsprache ändern
In `index.html` sucht das Script `localStorage.getItem('lang') || 'tr'`.
Für Deutsch als Default: `|| 'de'` setzen.

### Countdown / ICS-Zeit korrekt einstellen
Event: **27. Juni 2026, 16:00 Uhr Ortszeit Ratingen** (Sommerzeit, UTC+2)
→ in UTC: `2026-06-27T14:00:00Z` (bereits so konfiguriert).
Ende 22:00 Ortszeit → `2026-06-27T20:00:00Z`.

Wenn ihr das Datum ändert und nicht sicher seid, ob Sommer-/Winterzeit: einfach die Ortszeit wie „16:00" lassen und dann entsprechend 2h (Sommer) oder 1h (Winter) abziehen, um den UTC-Wert zu bekommen.

---

## Dateistruktur

```
/
├── index.html              ← alles inline (HTML + CSS + JS)
├── couple.jpeg             ← Paar-Foto
├── assets/
│   └── illustration.svg    ← Hero-Hintergrund-Illustration
└── README.md               ← dieses Dokument
```

---

Viel Freude an dem Fest! 🌿
