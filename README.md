# Record-high sea level off Vancouver Island

Web page that asks what raised sea level off Bamfield, Vancouver Island, in autumn 2026, using DUACS satellite
altimetry and ERA5 winds for the Northeast Pacific (35–60°N, 150–120°W).

Live page: <https://giulianab.github.io/dual-nepac/>

## Story

1. **The highest sea level on record off Bamfield.** Daily SSHA time series, 1993 to present, with its daily
   climatology and the 1993–2025 linear trend.
2. **Downwelling-favorable winds played a role.** ERA5 10 m wind maps: climatology for the same days, current
   period, and the alongshore wind in the time series.
3. **The local wind alone cannot explain the rise.** Cross-correlation and 10-day block means of sea level vs.
   alongshore wind (linear trend removed).
4. **No clear propagation of a wave along the coast.** Hovmöller of the daily sea level anomaly along the 200 m
   isobath, 35–55°N (seasonal cycle removed, trend not removed).
5. **Day by day.** Video: SSHA map with winds, SSHA off Bamfield, and SSHA along the isobath.

## Files in `site/`

| File | Content | Made by |
|---|---|---|
| `index.html` | the page | edited by hand |
| `ssha_bamfield.csv` | daily SSHA off Bamfield and alongshore wind, with their daily climatologies | `make_site.py` |
| `meta.json` | grid points, dates, video version stamp | `make_site.py` |
| `ssha_bamfield.mp4` | video, re-encoded for the web (keyframe every 10 frames) | `ssha_hovmoller_video.py` → `make_site.py` |
| `wind_maps.png`, `wind_maps.json` | ERA5 wind maps (section 2) | `make_wind_maps.py` |
| `wind_diagnostic.png`, `wind_diagnostic.json` | wind vs. sea level diagnostic (section 3) | `wind_sealevel_diagnostic.py` → `make_site.py` |
| `hovmoller_anom.png`, `hovmoller_anom.json` | Hovmöller of the anomaly (section 4) | `make_hovmoller.py` → `make_site.py` |

The `.json` files carry a `generated` stamp; the page adds it to the image and video addresses so browsers
always load the newest version.

## Update

From the `el_ninio` folder:

```bash
python ssha_hovmoller_video.py        # video  -> ssha_bamfield_<year>.mp4
python make_wind_maps.py              # wind maps -> site/
python wind_sealevel_diagnostic.py    # section 3 figure -> figures/
python make_hovmoller.py              # section 4 figure -> figures/
python make_site.py                   # CSV, meta.json, web video, copies the figures into site/
cd site
git add -A
git commit -m "Update data"
git push
```

GitHub Pages refreshes the site in a minute or two. Browsers may keep the old page for up to about 10 minutes;
use a forced reload (Cmd+Shift+R) or a private window to check.

## Methods (short)

- **SSHA** = DUACS SLA minus its 1993–2025 time mean, at the grid point nearest Bamfield.
- **Daily climatology**: mean of each calendar day over 1993–2025, smoothed with a centered, circular running
  mean of 10 days (climatologies drawn on the page and Hovmöller).
- **Alongshore wind**: ERA5 10 m wind projected onto 315° (toward the northwest, poleward); positive =
  downwelling-favorable.
- **Section 3**: daily SSHA and alongshore wind (the series of section 1), slope of the 1993–2025 linear trend
  removed from all years; cross-correlation at lags 0–30 days; then the wind is shifted by the best lag and both
  series are averaged in consecutive 10-day blocks.
- **Section 4**: daily SSHA along the 200 m isobath minus the daily climatology of each point; trend not removed.

## Data

- Sea level: Copernicus Marine Service, DUACS L4 0.125° daily (MY where available, NRT for the most recent days).
- Wind: ECMWF ERA5 hourly 10 m wind (u10, v10), averaged per day.
- Bathymetry: ETOPO1.

Author: Giuliana Berden.
