# datafun-06-applied

[![Python 3.14](https://img.shields.io/badge/python-3.14%2B-blue?logo=python)](./pyproject.toml)
[![MIT](https://img.shields.io/badge/license-see%20LICENSE-yellow.svg)](./LICENSE)

> Professional Python project: applied data analytics.

## What This Project Does

This project performs Exploratory Data Analysis (EDA) using Jupyter notebooks.
It includes two notebooks:

- **eda_case.ipynb** — the provided OWID CO2 emissions example, modified to add
  a time-trend chart showing CO2 per capita over time by country
- **eda_dynon.ipynb** — a custom EDA applying the same workflow to real Dynon
  avionics flight data, grouped by altitude band

Both notebooks follow the same structure: load data, inspect, clean, compute
descriptive statistics, build a correlation matrix, and visualize relationships.

## Setup

```shell
git clone https://github.com/j-carne/datafun-06-applied
cd datafun-06-applied
uv sync --extra dev --extra docs --upgrade
uvx pre-commit install
```

## How to Run

Open either notebook in VS Code and select the `.venv` kernel, then **Run All**:

- `notebooks/eda_case.ipynb`
- `notebooks/eda_dynon.ipynb`

Both notebooks end with:

```shell
========================
Executed successfully!
========================
```

A `project.log` file will appear in the root project folder with detailed run output.

## OWID CO2 Example — Key Results

Correlation matrix highlights:

| Variables | Correlation | Interpretation |
|-----------|-------------|----------------|
| co2 & gdp | 0.98 | Larger economies emit more total CO2 |
| co2 & population | 0.95 | Larger populations emit more total CO2 |
| co2_per_capita & gdp | -0.05 | Wealth doesn't predict individual emissions |

Per-capita CO2 by country (2022):

| Country | CO2 per Capita |
|---------|-----------------|
| United States | 21.4 |
| Canada | 18.3 |
| Germany | 8.4 |
| World Average | 4.6 |
| India | 1.3 |

**Custom modification:** Added a line chart tracking CO2 per capita over time
for each country, revealing that the US and Canada have remained consistently
highest throughout the dataset, while China's per-capita emissions rose steadily.

## Dynon Flight Data — Custom Project

Real avionics data recorded during a general aviation flight: 14,131 samples
covering pressure altitude, indicated airspeed, vertical speed, OAT, and RPM.
Grouped by altitude band (2000-4000 ft, 4000-6000 ft, Above 6000 ft).

### Correlation Matrix

| Variables | Correlation |
|-----------|-------------|
| RPM & Airspeed | 0.89 |
| Altitude & OAT | -0.66 |
| Altitude & RPM | 0.55 |
| Altitude & Airspeed | 0.49 |

### Key Finding

Altitude and airspeed show only a **moderate** correlation (0.49) — weaker than
expected. RPM is a far stronger predictor of airspeed (0.89). The scatter plot
shows each altitude band spans a wide range of airspeeds, suggesting flight
phase (climb vs. cruise) drives airspeed more than altitude itself.

![Altitude vs Airspeed Scatter Plot](./docs/images/altitude_vs_airspeed.png)

OAT showed a strong negative correlation with altitude (-0.66), consistent
with the standard atmospheric lapse rate — a good sanity check that the data
and methodology are sound.

## Project Documentation

[docs/index.md](docs/index.md)

## Notes

- `data/raw/dynon_data.csv` is kept local and not pushed to GitHub
- Use the **UP ARROW** and **DOWN ARROW** in the terminal to scroll through past commands
- If you see `>>>` or `...` in your terminal, you accidentally started Python interactive
  mode — press `Ctrl+c` or `Ctrl+Z` then `Enter` on Windows

## Citation

[CITATION.cff](./CITATION.cff)

## License

[MIT](./LICENSE)
