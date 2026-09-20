# Stallion Build Tracker

**Live app:** https://neil293.github.io/stallion-build-tracker/

A print/build checklist PWA for the Flightory "Stallion" V2 + VTOL RC aircraft.
Tracks which 3D-printed parts you've printed, lets you filter by section/filament,
and has a Settings page for the build's configurable options (nose variant,
wingtip LED, V-Tail servo orientation, motor mount size, tail configuration).

State (checked parts + settings) is saved in the browser's local storage on
each device — there's no backend, so it doesn't sync between your phone and
computer. If you want that later, the original app brief already scoped a
Firebase-backed version; ask and it can be added.

## Running it

It's a static site — `index.html`, `manifest.json`, `sw.js`. No build step.

- **Locally:** open `index.html` directly, or serve the folder with any static
  server (e.g. `python3 -m http.server`) — a real HTTP(S) origin is required
  for the service worker (offline support) to register.
- **GitHub Pages:** see below.

## One-time setup: GitHub Pages

1. In this repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.
4. Wait a minute, then your app is live at:
   https://neil293.github.io/stallion-build-tracker/

## Installing on your devices

- **Android (Chrome):** open the Pages URL, tap the menu (⋮) → **Install app**.
- **iPhone/iPad (Safari):** open the Pages URL, tap **Share** → **Add to Home
  Screen**.
- **Desktop (Chrome/Edge):** open the Pages URL, click the install icon (⊕)
  in the address bar.

Once installed it opens full-screen like a native app and keeps working
offline (the app shell and your data are cached on-device).

## Photos

Every part has a small camera button that opens a photo. Five VTOL-conversion
parts (wing panels, booms, motor mounts) already show a rendered preview
generated from their STL files, in `images/`.

For everything else, tapping the button just tells you which file it's
looking for, e.g. `images/fus-1.jpg`. To add a real photo of a part once
you've printed it: drop a `.jpg` or `.png` into `images/` named after that
part's id (the id is whatever the message names — no code changes needed),
commit and push. It'll show up automatically next time the button is tapped.

## Updating the app

Edit `index.html` (parts list is the `PARTS` array near the top of the
`<script>`), bump `CACHE_VERSION` in `sw.js` so installed devices pick up the
change, commit and push. GitHub Pages redeploys automatically within a
minute or two.
