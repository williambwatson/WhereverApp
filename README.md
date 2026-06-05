# Wherever 🍽️

A tiny web app for when neither of you can pick a place to eat. It grabs your current
location, finds restaurants nearby — with **photos, ratings, a short description, and a real
review snippet** — and lets you **swipe** until one feels right. Pick one → tap **Open in
Maps** → go.

The entire app is a single `index.html` — no build step — so you can edit it from your phone.

## One-time setup

### 1. Get a Google Places API key
The photos/ratings/reviews come from Google, which needs a free key:

1. Go to <https://console.cloud.google.com/> and create a project (any name).
2. **Enable billing** (Billing → link a card). Personal use stays inside Google's free monthly
   allowance, so you should not actually be charged — but Google requires a card on file.
3. **APIs & Services → Library** → enable **Places API (New)** and **Maps JavaScript API**.
4. **APIs & Services → Credentials → Create credentials → API key.** Copy it.
5. Click the new key to restrict it (recommended):
   - **Application restrictions → Websites** → add `https://<your-username>.github.io/*`
   - **API restrictions → Restrict key** → check **Places API (New)** and **Maps JavaScript API**
   - Save. (The referrer restriction is what keeps the key safe even though it's visible in the
     page — only your site can use it.)

### 2. Paste the key into the app
Open `index.html` and find this line near the top:

```js
window.GOOGLE_PLACES_KEY = "PASTE_YOUR_KEY_HERE";
```

Put your key between the quotes. That's the only line you need to change.

### 3. Put it online (GitHub Pages, free HTTPS)
Location only works over HTTPS, which Pages gives you free:

1. In your repo, **Settings → Pages** → Source **Deploy from a branch** → **main / root** → Save.
2. Live at `https://<your-username>.github.io/<repo-name>/` in ~30s.
3. Send that link to your partner — you'll both be on the same app.

## Edit it from your iPhone
1. Open the repo in Safari → tap `index.html` → tap the **pencil** (Edit) icon.
2. Make your change → **Commit changes**.
3. Pages redeploys automatically. Refresh the live URL in ~30s to see it.

## How it works
- **Location:** the browser's Geolocation API (asks permission on first tap).
- **Restaurants:** Google **Places API (New)** — nearby search for the most popular restaurants,
  with photo, rating, price, and a description. One review per place is loaded only when you look
  at its card, to keep API usage tiny.
- **Open in Maps:** uses Google's canonical link for the exact place, so it opens cleanly on iPhone.

## Tweaking it
A few easy knobs near the top of the main `<script>` in `index.html`:
- `RADII` — the search distances (in metres) it steps through (2 km → 5 km → 12 km).
- `MAX_CARDS` — how many spots to load per search (Google returns up to 20).
- Colors live in the `:root` CSS block at the top (`--ember`, `--wine`, etc.).

## Costs, honestly
For two people deciding dinner, you'll make a handful of calls a day — comfortably inside
Google's free monthly limits, so realistically **$0**. If you ever wanted to remove the card-on-file
requirement entirely, the trade-off is losing photos and reviews (the free/keyless data sources
don't include them).
