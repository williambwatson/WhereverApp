# Wherever 🍽️

A tiny web app for when neither of you can pick a place to eat. It grabs your current
location, finds restaurants nearby (via free OpenStreetMap data — no API key), and lets
you **swipe** until one feels right. Pick one → tap **Open in Apple Maps** → go.

The entire app is a single `index.html` — no build step, no dependencies — so you can edit
it straight from your phone.

## Try it locally
Just open `index.html` in a browser. **Note:** location only works over HTTPS, so for the
real GPS experience you need to host it (below). On `localhost` most browsers also allow it.

## Put it online (one-time, ~3 minutes)
Location requires HTTPS, and GitHub Pages gives you that for free:

1. Create a **public** repo on GitHub (e.g. `wherever`) and upload `index.html`.
2. Repo → **Settings → Pages** → Source: **Deploy from a branch** → **main / root** → Save.
3. Wait ~30s. Your app is live at `https://<your-username>.github.io/wherever/`.
4. Send that link to your partner — you'll both be on the exact same app.

## Edit it from your iPhone
1. Open the repo in Safari → tap `index.html` → tap the **pencil** (Edit) icon.
2. Make your change → **Commit changes**.
3. GitHub Pages redeploys automatically. Refresh the live URL in ~30s to see it.

## How it works
- **Location:** the browser's Geolocation API (asks permission on first tap).
- **Restaurants:** the [Overpass API](https://overpass-api.de) querying OpenStreetMap for
  `amenity=restaurant`/`fast_food` around you. Default search ~2 km, widening to 5 km then 12 km
  if nothing's found.
- **No accounts, no keys, no tracking.** It only ever uses your location to run the search.

## Tweaking it
A few easy knobs near the top of the `<script>` in `index.html`:
- `RADII` — the search distances (in metres) it steps through.
- `MAX_CARDS` — how many spots to load per search.
- Colors live in the `:root` CSS block at the top (`--ember`, `--wine`, etc.).
