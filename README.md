# Record-high sea level off Vancouver Island

Web page that asks what raised sea level off Bamfield, Vancouver Island, in autumn 2026, using DUACS satellite
altimetry and ERA5 winds for the Northeast Pacific (35–60°N, 150–120°W).

Live page: <https://giulianab.github.io/dual-nepac/>


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

- Sea level: Copernicus Marine Service, DUACS L4 0.125° daily (MY where available, NRT for the most recent days).
- Wind: ECMWF ERA5 hourly 10 m wind (u10, v10), averaged per day.
- Bathymetry: ETOPO1.

Author: Giuliana Berden.
