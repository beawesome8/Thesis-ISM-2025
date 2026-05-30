# Thesis-ISM-2025

# Analyzing and Predicting Urbanization Patterns in Germany Using Data Mining Techniques

**Master's Thesis** — International School of Management (ISM), Munich  
**Author:** Aman Benjamin Emmanuel  
**Degree:** MSc Business Intelligence & Data Science  
**Submission:** July 2025  
**Supervisors:** Prof. Dr. Patrick Schmid · Prof. Dr. Andreas Widenhorn

---

## Overview

This repository contains the research code and datasets supporting my Master's thesis on urbanization forecasting in Germany. The study combines classical time-series forecasting, deep learning, and unsupervised clustering to analyze how Germany's urban population has evolved from 1990 to 2023, and to project it through 2043.

The research is structured around three phases:

1. **Predictive time-series forecasting** — ARIMA baseline and multivariate LSTM neural network to forecast national urbanization rates.
2. **Exploratory cross-sectional clustering** — K-Means clustering of all 16 German federal states by socio-economic and environmental indicators (2023 data).
3. **Integrative mixed approach** — Disaggregating national LSTM forecasts into cluster-level projections for regional planning insights.

---

## Key Findings

- Germany's urban population share grew steadily from ~73% in 1990 to ~78% in 2023 (+0.17 percentage points/year on average).
- The multivariate LSTM outperformed the ARIMA baseline with a test RMSE of **0.228 pp** vs. **0.523 pp**, and near-identical MAPE of ~0.29%.
- The LSTM projects Germany's urban share to reach **~81.3% by 2043** under baseline conditions, and up to **~82.7%** under high-growth scenarios.
- K-Means clustering (k=3) identified three distinct urbanization typologies across Germany's 16 federal states:
  - **Highly Urbanized** — Berlin, Hamburg, Bremen, Hesse (~17.4% of national urban population)
  - **Urbanized Hubs** — Bavaria, Baden-Württemberg, North Rhine-Westphalia (~53.2%)
  - **Mixed Urban–Rural** — remaining 10 states (~29.4%)
- Key policy thresholds: employment rate ≥68%, tertiary education ≥22%, and per-capita waste ≤620 kg/year emerged as inflection points for urban growth.

---


## Data Sources

| Source | Variables |
|--------|-----------|
| [Destatis](https://www.destatis.de) | Population, net migration, house price index, CPI, health expenditure |
| [Eurostat](https://ec.europa.eu/eurostat) | Employment rate, tertiary education, GHG emissions, waste generated |
| [Our World in Data](https://ourworldindata.org) | Urban and rural population splits |
| [IMF](https://www.imf.org) | GDP per capita (PPP, constant prices) |
| [WHO](https://www.who.int) | Land area |
| [Numbeo](https://www.numbeo.com) | State-capital quality-of-life indicators (for clustering) |
| [Deutschland.de](https://www.deutschland.de) | State-level land area |

All data covers the period **1990–2023** for the forecasting dataset and **2023** (cross-sectional) for the clustering dataset.

---

## Methodology

### Phase 1 — Time-Series Forecasting

- **ARIMA (0,1,1):** Stationarity confirmed via ADF and KPSS tests; model selected by minimizing AIC; residuals validated with the Ljung-Box test.
- **Multivariate LSTM:** Two-layer stacked architecture (PyTorch), trained on 10 standardized socio-economic and environmental predictors using a 5-year sliding window. Early stopping at epoch 19 (200 max). Adam optimizer, learning rate 0.001.
- **Scenario analysis:** Shock experiments applying ±10–300% multipliers to migration, GDP, and health expenditure inputs to test forecast sensitivity.

### Phase 2 — Clustering

- **K-Means (k=3):** Optimal k selected via elbow plot and silhouette score (0.25). 20 random restarts for stability. Features standardized to zero mean and unit variance.
- **DBSCAN:** Tested as validation; found ineffective on the small 16-state dataset (most states classified as noise).

### Phase 3 — Regional Disaggregation

- Each cluster's fixed 2023 share of national urban population is applied to the LSTM's national forecast, producing cluster-level growth trajectories through 2043.

---

## Installation & Setup

**Requirements:** Python 3.13+

```bash
# Clone the repository
git clone https://github.com/your-username/germany-urbanization-thesis.git
cd germany-urbanization-thesis

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook
```

### requirements.txt

```
pandas
numpy
matplotlib
seaborn
statsmodels
stationarity-toolkit
torch
scikit-learn
geopandas
shapely
plotly
jupyter
```

---

## Model Performance

| Model | Test RMSE (pp) | Test MAPE (%) |
|-------|---------------|---------------|
| ARIMA (0,1,1) | 0.523 | 0.293 |
| Multivariate LSTM | 0.228 | 0.294 |

Test period: 2017–2023. Rolling-window cross-validation average error: 0.24 pp.

---

## Datasets

The raw datasets are also available on Google Drive:

- [Forecasting Dataset (1990–2023)](https://docs.google.com/spreadsheets/d/19GCTVEqC6RRAazpsZ9wQkrYXwmvqpxw/)
- [Clustering Dataset (2023 State-Level)](https://docs.google.com/spreadsheets/d/1pooS7kDHTApShkmvsINaf8bZTsOltiM/)

---

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license.

You are free to share and adapt this work for non-commercial purposes, as long as you give appropriate credit to the author.

See [LICENSE](LICENSE) for full terms, or visit [creativecommons.org/licenses/by-nc/4.0](https://creativecommons.org/licenses/by-nc/4.0/).

---

## Citation

If you use or reference this work, please cite it as:

```
Emmanuel, A. B. (2025). Analyzing and predicting urbanization patterns in Germany
using data mining techniques [Master's thesis]. International School of Management,
Munich.
```

---


