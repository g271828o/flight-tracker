# ✈️ Flight Tracker

A mobile-friendly, single-page web app for tracking your flights and delays — built to work great on a phone.

## Features

- **Log your flights** — airline, flight number, origin/destination airports, scheduled vs. actual departure/arrival times.
- **Automatic delay calculation** — on-time / delayed badges, minutes late, per-leg delay breakdown.
- **Delay reason tracking** — using the standard US DOT/BTS categories (Air Carrier, Extreme Weather, National Aviation System, Late-Arriving Aircraft, Security).
- **Live airport weather & delay-risk** — for both origin and destination, pulled live from [Open-Meteo](https://open-meteo.com/) (no API key needed), with a low/moderate/high risk indicator and a plain-English explanation (e.g. "thunderstorms", "high wind", "low visibility").
- **Airport lookup** — search ~110 major world airports by city, name, or IATA code for name, location, and current conditions.
- **Stats dashboard** — on-time rate, average delay, delay-by-flight and delay-reason charts (D3.js).
- **Everything stored locally** — your data lives in your browser's local storage; export/import as JSON to back up or move devices.

## Running it

This is a static app — no build step, no server-side code, no API keys required.

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser. On your phone, open the same URL (if hosted, e.g. via GitHub Pages) and use "Add to Home Screen" for an app-like experience.

## Data sources

- Flight details are entered manually by you.
- Weather comes live from Open-Meteo's forecast and historical archive APIs (free, no key, CORS-enabled) — matched to each airport's local time zone.
- A handful of well-known major airports include a short general note about common delay causes (e.g. congestion, seasonal weather) — for context only, not live data.
