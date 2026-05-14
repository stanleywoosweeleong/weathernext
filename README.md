# 农友天气 WeatherNext

> Bilingual smart-farming Progressive Web App for Malaysian agriculture
> 马来西亚农业智能天气预报 PWA

![Theme](https://img.shields.io/badge/theme-%231d4ed8-1d4ed8?style=flat-square)
![PWA](https://img.shields.io/badge/PWA-installable-success?style=flat-square)
![Offline](https://img.shields.io/badge/offline-supported-success?style=flat-square)
![Languages](https://img.shields.io/badge/languages-5-blue?style=flat-square)

Hyperlocal 14-day forecasts for 60+ Malaysian farming locations with AI-powered agronomy briefings, work-plan generation, pest/disease risk analysis, and irrigation calculations. Built specifically for durian, rice, and oil palm growers.

## Features

- **14-day hourly forecasts** for 60+ pre-loaded West & East Malaysia farm locations, plus unlimited custom locations.
- **Dual weather models** — ECMWF IFS (default) and Open-Meteo Best Match (AI ensemble).
- **AI agronomy suite** powered by Gemini — smart briefings, pest risk analysis, 3-day work plans, SOP checklists, irrigation calculator, harvest predictor, soil/fertilizer advisor, yield insights.
- **5 languages** — English, Bahasa Malaysia, 中文, தமிழ், မြန်မာ.
- **Crop-aware** — switches between Durian, Rice/Vegetable, and Oil Palm advice profiles.
- **Cloud sync** via Firebase — favorites, custom locations, and renames sync across devices.
- **PWA install** — works offline, installs to home screen on Android/iOS/Desktop.
- **Image export** — generates branded forecast infographics for sharing on WhatsApp.

## Live demo

After enabling GitHub Pages (see below), this will be live at:

```
https://<your-username>.github.io/<repo-name>/
```

## Quick deploy to GitHub Pages

1. **Create a new GitHub repository** (public, no README/license/gitignore — keep it empty).
2. **Upload all files** in this folder to the root of the repo:
   - Use GitHub's web UI: drag-and-drop the entire folder contents into the empty repo, commit.
   - Or via Git CLI:
     ```bash
     git init
     git add .
     git commit -m "Initial PWA deployment"
     git branch -M main
     git remote add origin https://github.com/<your-username>/<repo-name>.git
     git push -u origin main
     ```
3. **Enable Pages**: Repo → **Settings** → **Pages** → Source: **Deploy from a branch** → Branch: **main** / Folder: **/ (root)** → **Save**.
4. **Wait ~1 minute** for the first build. The site URL will appear at the top of the Pages settings page.
5. **Open the URL on your phone**, wait 2-3 seconds, and the install banner will appear. Tap **Install**.

## Required first-time setup

After installing, the app will prompt for a **Gemini API key** the first time you tap an AI feature. Get a free key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey). The key is stored locally on your device only.

## File structure

```
.
├── index.html               # The PWA itself
├── manifest.json            # PWA manifest (icons, name, theme, shortcuts)
├── sw.js                    # Service worker (offline + smart caching)
├── icon-192.png             # Standard PWA icon
├── icon-512.png             # Standard PWA icon (high-res)
├── icon-maskable-192.png    # Android adaptive icon
├── icon-maskable-512.png    # Android adaptive icon (high-res)
├── apple-touch-icon.png     # iOS home-screen icon
├── favicon-32.png           # Browser tab icon
├── .nojekyll                # Tells GitHub Pages to skip Jekyll processing
└── README.md                # This file
```

## Caching strategy

The service worker uses different strategies per request type:

| Request | Strategy | Why |
|---|---|---|
| App shell (HTML, icons) | Cache-first | Instant load, fully offline |
| Tailwind / html2canvas CDN | Cache-first + bg revalidate | They rarely change |
| Open-Meteo weather API | Network-first → cache fallback | Fresh data wins, stale > nothing |
| Firebase / Gemini APIs | Network-only | Auth and AI must always be fresh |

Weather cache is capped at ~30 entries (LRU) to prevent unbounded growth.

## Updates

To deploy a new version after editing:

1. Make changes to `index.html`.
2. **Important**: open `sw.js` and bump the version line:
   ```js
   const CACHE_VERSION = 'wnext-v1.0.0';  // → 'wnext-v1.0.1'
   ```
3. Commit and push. GitHub Pages rebuilds in ~1 minute.
4. Users see a green "**New version ready · Reload**" banner the next time they open the app.

Without the version bump, users' cached service workers will keep serving the old assets.

## Browser compatibility

- **Chrome / Edge / Brave** (Android & Desktop) — full PWA install support, all features.
- **Safari** (iOS) — install via Share → Add to Home Screen; the app shows an iOS-specific install hint.
- **Firefox** — works as a PWA but no install prompt in v126+. Manual bookmark works fine.
- **Samsung Internet** — full PWA support including install.

## Tech stack

- Vanilla HTML / CSS / JS (no build step required)
- [Tailwind CSS](https://tailwindcss.com) via CDN
- [Firebase](https://firebase.google.com) — Auth & Firestore for cloud sync
- [Open-Meteo](https://open-meteo.com) — Free weather data (ECMWF IFS, Best Match)
- [Gemini API](https://ai.google.dev) — AI agronomy features
- [html2canvas](https://html2canvas.hertzen.com) — Forecast image export

## License

Personal/agricultural use. Not for redistribution without permission.

---

Built for LV LONG SDN. BHD. agricultural workflows.
