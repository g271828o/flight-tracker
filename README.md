# ✈️ Flight Tracker

A mobile-friendly, single-page web app for tracking your flights and delays — built to work great on a phone.

## Features

- **Log your flights** — airline, flight number, origin/destination airports, scheduled vs. actual departure/arrival times.
- **Automatic delay calculation** — on-time / delayed badges, minutes late, per-leg delay breakdown.
- **Delay reason tracking** — using the standard US DOT/BTS categories (Air Carrier, Extreme Weather, National Aviation System, Late-Arriving Aircraft, Security).
- **Live airport weather & delay-risk** — for both origin and destination, pulled live from [Open-Meteo](https://open-meteo.com/) (no API key needed), with a low/moderate/high risk indicator and a plain-English explanation (e.g. "thunderstorms", "high wind", "low visibility").
- **Airport lookup** — search ~110 major world airports by city, name, or IATA code for name, location, and current conditions.
- **Live position tracking** — on a flight's detail page, tap "Track live position" to see its current altitude, speed, heading, and location in the air, pulled live from [OpenSky Network](https://opensky-network.org/) (free, no signup).
- **Optional full live status** — scheduled/estimated/actual times, delay minutes, and gate, from an AviationStack-compatible provider you configure yourself in Settings with your own API key (stored only in your browser).
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
- Live position comes from OpenSky Network's public state-vector API (free, no key). Matching works by converting your flight's airline code + number (e.g. `UA 523`) into an ICAO callsign (`UAL523`) using a bundled airline table, then looking for that callsign among currently-tracked aircraft — so it only finds a match while the flight is actually airborne and broadcasting ADS-B.
- Full live status (schedule/delay/gate) is opt-in: add your own AviationStack (or compatible) API key and base URL under Settings. It's stored only in `localStorage` and sent only to the URL you configure. Note that AviationStack's free plan is HTTP-only, which browsers block from this HTTPS-hosted site — either upgrade to a plan with HTTPS, or point Base URL at your own HTTPS proxy (e.g. a small serverless function).
- A handful of well-known major airports include a short general note about common delay causes (e.g. congestion, seasonal weather) — for context only, not live data.
