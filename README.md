# Arclight — Home Screen web app

This is a self-contained, installable version of Arclight. No app store, no build step —
just static files (`index.html`, `manifest.json`, `sw.js`, icons).

## What changed from the original component

- Bundled into one `index.html` — React, Recharts, and the icon set load from CDNs at
  runtime; your JSX compiles in the browser (via Babel standalone), so there's nothing to build.
- Replaced `lucide-react` with a small hand-rolled icon set (same names, same call sites)
  so the app has one less dependency to fetch.
- **Data now actually persists.** Your tasks, habits, goals, notes, journal, and mood entries
  save to `localStorage` automatically (the Settings screen already claimed this — now it's true).
- Added `manifest.json` + `sw.js` so the app can be installed to a phone's home screen and
  launches full-screen, without a browser address bar, and keeps working with no signal
  after the first load.

## Host it (required for the install prompt + offline support to work)

Opening `index.html` by double-clicking it will run the app, but phones only offer "Add to
Home Screen" as a real install (with offline caching) for pages served over **https**. Any
static host works — pick whichever is easiest:

- **Netlify Drop** — go to https://app.netlify.com/drop and drag the whole `arclight` folder in.
  You'll get a live https URL in a few seconds, no account needed.
- **GitHub Pages** — push this folder to a repo, enable Pages on the `main` branch, done.
- **Vercel / Cloudflare Pages** — same idea, drag-and-drop or connect a repo.

Keep all the files in the same folder — `index.html` links to `manifest.json`, `sw.js`, and
the icon PNGs by relative path.

## Install it on your phone

**iPhone (Safari):** open the hosted URL → Share icon → **Add to Home Screen**.
**Android (Chrome):** open the hosted URL → ⋮ menu → **Add to Home screen** / **Install app**.

Once installed, it opens in its own window (no browser chrome), gets its own icon, and after
the first load will keep working offline.

## Notes

- All your data lives in that browser's `localStorage` on that device — it doesn't sync
  between devices or between "installed app" and "browser tab." Settings → Export data (JSON)
  gives you a portable backup any time.
- If you want a different app icon, swap `icon-192.png`, `icon-512.png`,
  `icon-512-maskable.png`, and `apple-touch-icon.png` for your own (same filenames/sizes).
