# Dozy

A one-tap sleep and feeding log. Sleep, Wake, Eat and Finished plot on a scrollable day timeline, and dashed
windows predict the next nap, bedtime and meal. Predictions start from the numbers you enter under the gear icon
and shift toward what actually happens as days are logged.

It is a plain static web app (installable PWA). No build step, no backend. Data stays on the phone.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `manifest.webmanifest` | Name, icons and colors for install |
| `sw.js` | Service worker, so it opens offline |
| `icons/` | App icons (any, maskable, Apple touch) |

## Deploy on GitHub Pages

1. Push this repo to GitHub.
2. Repo **Settings → Pages → Build and deployment → Deploy from a branch**, pick `main` and `/ (root)`.
3. After a minute the app is at `https://<user>.github.io/dozy/`.

Any static host works the same way (Netlify, Cloudflare Pages, Vercel). It must be served over HTTPS to install.

## Install on Android

Open the link in Chrome, then menu **⋮ → Install app** (or **Add to Home screen**). It opens full screen with its own icon.

## Updating

Phones keep a cached copy. When you change anything, bump `CACHE` in `sw.js` (for example `dozy-v2`) and deploy.
The new version loads the next time the app is opened.

## Run locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Service workers work on `localhost` without HTTPS.

## Data

Events are stored in the browser's `localStorage` as `{ t: "sleep" | "eat", s: startMs, e: endMs | null }`.
Use **Settings → Back up data** to download a JSON copy and **Restore backup** to load one. Clearing the browser's
site data deletes the log, so back up first. Moving to a new phone is a backup and restore.

## Not included yet

- Notifications when a window opens (needs a push server, or the Capacitor wrapper for local notifications)
- Home-screen widget (needs a native app)
- Syncing between two phones (needs a backend)
