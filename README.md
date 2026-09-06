# SENTINEL-9 — Global Situational Awareness Console

A single-file, zero-build browser console that tracks satellites with real orbital
mechanics and triages public news feeds on the same map. Open the HTML file and it runs.

Everything in it is open-source data. Nothing is classified, nothing is operational —
the classification bar says so, and the reference panel (`?`) spells out which numbers are
computed, which are keyword-guessed, and which are simulated.

---

## Quick start

```bash
# just open it
open sentinel9-global-situational-awareness-console.html

# or serve it (recommended — some proxies behave better over http)
python3 -m http.server 8080
# → http://localhost:8080/sentinel9-global-situational-awareness-console.html
```

No install, no npm, no bundler. One HTML file, ~122 KB.

**First 30 seconds:** the boot sequence pulls element sets, selects the ISS, and starts
propagating at 1 Hz. Press `Ctrl K` and type `track hubble`, or click a ground station in
the GROUND tab to set an observer site and get pass predictions.

---

## What it does

### Orbital engine

| Capability | Detail |
|---|---|
| Propagation | SGP4 via `satellite.js` when the CDN loads; otherwise a Kepler + J2-secular propagator built into the file |
| Element sets | Live from CelesTrak (`stations`, `visual`, `weather`, `geo`), up to 110 objects |
| Offline fallback | 30 cached mean-element objects carried in the file; status bar shows `CACHED` in amber |
| Per-object solution | Sub-point, altitude, velocity, period, inclination, footprint diameter, orbital phase |
| Ground tracks | ±0.6 orbit, antimeridian-split, with the next 30 min emphasised |
| Footprints | Horizon circle from `acos(Rₑ/(Rₑ+h))`, plus a half-radius ring and a line-of-sight line to the observer |
| Pass prediction | 24 h sampled at 30 s; reports AOS, LOS, max elevation, duration, azimuth, live T− countdown |

Numbers were validated before shipping — ISS at 414.8 km / 7.661 km/s, GOES-16 holding
35,789 km with 0.006° drift over 6 h, a Molniya HEO swinging 1,116 → 39,300 km, and 4
NOAA-19 horizon crossings per day over Dhaka. All correct.

### Map

Four basemaps (imagery, dark, terrain, relief) and eight toggleable overlays: satellites,
ground tracks, footprints, computed solar terminator with subsolar point, 16 real public
ground stations, geolocated report clusters, graticule, place labels. Great-circle range
tool gives distance in km and nmi plus forward and reverse bearing.

### OSINT pipeline

Eight public RSS sources → CORS proxy chain → dedupe → classify → geotag → render.

- **Severity** by keyword match: critical / elevated / routine
- **Tags**: SPACE, CYBER, MILITARY, CLIMATE, ECONOMY, HEALTH, ENERGY
- **Geotagging** against ~90 place names, so reports cluster on the map and drive a
  theatre-activity breakdown
- **Alert queue**: critical items auto-promote, with an audio cue and per-item acknowledge

Refresh runs every 3 minutes, or on `R`.

### Analysis

Rolling threat index sparkline, severity donut, source-volume bars, altitude-vs-inclination
scatter of the whole catalogue, theatre KPIs. All drawn on canvas — no chart library.

---

## Keyboard

| Key | Action | Key | Action |
|---|---|---|---|
| `Ctrl K` | Command palette | `C` | Coverage footprints |
| `R` | Refresh feeds | `L` | Follow selected object |
| `F` | Reset map view | `M` | Range measurement |
| `B` | Cycle basemap | `↑` `↓` | Previous / next track |
| `N` | Day–night boundary | `A` | Acknowledge top alert |
| `T` | Ground tracks | `Esc` | Close panel |

The command palette also parses free text: `goto 23.81, 90.41`, `track ISS`, `find starlink`,
or any place name in the gazetteer.

---

## Architecture

One file, three concerns, in order:

```
<style>          design tokens + all CSS
<body>           shell markup: classbar, header, rail, map stage, dock, footer, modals
<script>         ├─ core      helpers, state, orbital mechanics, cached element set
                 ├─ map       Leaflet setup, layers, terminator, rendering, measurement, passes
                 └─ app       feed pipeline, alerts, analytics, telemetry, palette, boot
```

State lives in one `state` object. No framework, no localStorage (so it works inside
sandboxed viewers too) — reload starts clean.

**External dependencies**, all optional and all degraded gracefully:

- Leaflet 1.9.4 (unpkg) — required for the map
- satellite.js 5.0.0 (cdnjs) — upgrades propagation to SGP4; falls back silently
- Esri / CARTO tiles — basemaps
- CelesTrak — element sets; falls back to the cached catalogue
- `allorigins` / `corsproxy` — RSS CORS relays; falls back to cached demo items

Boot waits at most 11 s for element sets, so a blocked network never hangs the splash.

---

## Configuration

All the knobs are plain arrays near the top of their section:

| Want to change | Edit |
|---|---|
| News sources | `FEEDS` |
| Severity keywords | `SEV_HIGH`, `SEV_MED` |
| Category tags | `TAGS` |
| Gazetteer | `PLACES` (`['name', lat, lon]`) |
| Ground stations | `SITES` |
| Satellite groups pulled | `TLE_GROUPS` |
| Offline catalogue | `CACHED` |
| Palette | `:root` custom properties |

Refresh cadences are the `setInterval` calls in `start()` — position 1 s, telemetry 2 s,
terminator 60 s, feeds 180 s.

---

## Known limits

- The **cached element set** uses plausible mean elements, not real current ones. Tracks
  from it drift from truth; that is why it is labelled and colour-coded.
- **Severity and geotagging are keyword heuristics.** Treat them as a triage hint, not a
  finding. "Turkey" matches a country whether or not the article is about poultry.
- **Downlink, latency and packet loss are simulated** to exercise the telemetry strip.
- Pass prediction filters to objects below MEO plus the current selection, capped at 14
  objects, minimum 10° max elevation.
- Public CORS proxies are rate-limited and occasionally down. Feeds fall back; satellites
  keep running regardless.
- Above ~110 tracked objects the 1 Hz marker update starts to cost frames on low-end
  hardware. Raise the cap in `fetchTLEs()` if your machine can take it.

---

## Where to take it next

- **3D globe** — swap the Leaflet stage for three.js; the propagator already returns ECI
  state vectors, so the geometry is free.
- **Live telemetry** — replace `tickTelemetry()` with a WebSocket subscriber and the strip
  becomes real instead of simulated.
- **Doppler and link budget** — range rate is one finite difference away from what
  `elevationAt()` already computes.
- **Persistence** — observer sites, acknowledged alerts and layer state are all in `state`
  and would serialise in a few lines.
- **Conjunction screening** — pairwise range between catalogue objects at each tick,
  flagged below a threshold.

---

Built on the structure of the earlier Satellite Intelligence Center: same dark-console
lineage, real orbital mechanics underneath.
