# SSHA · Northeast Pacific

Web page with the daily DUACS sea surface height anomaly (SSHA) video for the Northeast Pacific (35–60°N, 150–120°W), with ERA5 10 m winds, and an interactive SSHA time series off Bamfield, Vancouver Island.

Live page: <https://giulianab.github.io/dual-nepac/>

## Files

- `index.html` – the page
- `ssha_bamfield.mp4` – video (made by `ssha_bamfield_video.py`)
- `ssha_bamfield.csv` – daily SSHA off Bamfield, 1993 to present (made by `make_site.py`)
- `meta.json` – grid point and dates shown on the page

## Update

From the `el_ninio` folder:

```bash
python ssha_bamfield_video.py     # new video
python make_site.py               # new CSV, copies the video into site/
cd site
git add -A
git commit -m "Update data"
git push
```

GitHub Pages refreshes the site in a minute or two.

## Data

- Sea level: Copernicus Marine Service, DUACS L4 0.125° daily (MY and NRT). SSHA = SLA minus its 1993–2025 time mean.
- Wind: ECMWF ERA5 10 m wind, daily mean.
