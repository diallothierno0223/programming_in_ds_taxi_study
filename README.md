# NYC Yellow Taxi Study — Programming for Data Science (ESILV)

Final project of the *Programming for Data Science* course (H. Alatrista-Salas).
We apply the **KDD process** to the NYC TLC Yellow Taxi trip records (May – July 2026, ~10 M trips)
and present the results in a **Dash dashboard**.

**Team:** Thierno DIALLO (team head), Joe VASEEKARAN, Lisandru ZUCCARELLI, Noé PAYAN

## Contents

| File | Description |
|---|---|
| `DIALLO_notebook.ipynb` | Main notebook: exploration, cleaning, 4 queries, dashboard, `__main__` block |
| `outputs/DIALLO_dashboard.html` | Static export of the dashboard (evidence that it works) |
| `data/` | Raw data (not versioned, see below) |
| `pyproject.toml`, `uv.lock` | Dependencies |

## The four queries

1. **Grouping** — revenue, demand and average card tip per pick-up zone / borough (top 10 zones).
2. **Frequent pattern mining** — Apriori + association rules on discretised trip attributes
   (boroughs, time slot, weekday/weekend, payment type, distance, tip level, passengers).
3. **Temporal forecasting** — hourly demand, Holt-Winters (weekly seasonality) trained on May–June,
   evaluated on July vs a seasonal-naive baseline (MAE, RMSE, MAPE).
4. **Spatial clustering** — K-Means on per-zone profiles (demand, distance, fare, night/weekend share,
   tip, centroid), k chosen with the silhouette score, shown on a choropleth map.

Every indicator is explained in a markdown cell of the notebook.

## Data

Download into `data/` (files are too large for Git):

- `yellow_tripdata_2026-05.parquet`, `yellow_tripdata_2026-06.parquet`, `yellow_tripdata_2026-07.parquet`
  from https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- `taxi_zone_lookup.csv` and the `taxi_zones/` shapefile (same page, "Taxi Zone Lookup Table" / "Taxi Zone Shapefile")

```text
data/
├── yellow_tripdata_2026-05.parquet
├── yellow_tripdata_2026-06.parquet
├── yellow_tripdata_2026-07.parquet
├── taxi_zone_lookup.csv
└── taxi_zones/taxi_zones.shp (+ .dbf, .shx, .prj, .cpg)
```

## Setup

With [uv](https://docs.astral.sh/uv/) (recommended):

```bash
uv sync
uv run --with jupyterlab jupyter lab   # or open the notebook in VS Code with the .venv kernel
```

With pip:

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install dash geopandas ipykernel mlxtend nbconvert nbformat numpy pandas plotly pyarrow scikit-learn shapely statsmodels jupyter
```

## Running

- **Interactively:** run all cells. The last cell starts the dashboard at http://127.0.0.1:8050.
- **Headless** (no dashboard server, only the HTML export):

```bash
RUN_DASHBOARD=0 uv run jupyter nbconvert --to notebook --execute --inplace DIALLO_notebook.ipynb
```

The notebook needs ~6 GB of RAM (three months of trips are loaded at once).
