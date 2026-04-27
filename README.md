# Predictive Crime Hotspot Modelling — SAPS Station-Level Analysis

> Forecasting future crime counts at police station level using an ML ensemble,  
> enabling proactive resource allocation across South Africa.

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)
![XGBoost](https://img.shields.io/badge/XGBoost-ensemble-orange?style=flat-square)
![LightGBM](https://img.shields.io/badge/LightGBM-ensemble-green?style=flat-square)
![Power BI](https://img.shields.io/badge/Power%20BI-dashboard-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

---

## Overview

This project builds an end-to-end machine learning pipeline to **forecast annual crime counts per SAPS police station** using 15 years of historical data (2008–2023). The goal is to shift policing strategy from reactive to proactive — identifying emerging hotspots before they escalate.

**Key result:** Achieved a mean absolute error (MAE) of ~200 crimes per station-year, providing actionable accuracy for real-world policing and resource planning.

---

## Business Impact

| Challenge | Solution |
|---|---|
| Reactive policing wastes resources | Forecasts enable patrol pre-deployment |
| Hard to spot emerging hotspots early | Top 20% high-risk stations flagged automatically |
| Manual reporting is slow | Power BI dashboard provides live station-level views |
| No forward planning for 2024 | 2024 crime forecasts generated per station |

---

## Technical Approach

### 1. Data pipeline (SQL)
- Extracted and aggregated raw SAPS station-level records via SQL queries
- Cleaned and validated 15 years of crime data across hundreds of stations
- Handled missing values, outliers, and inconsistent station naming

### 2. Feature engineering
- **Lag features** — prior year crime counts per station
- **Rolling averages** — 3-year and 5-year crime trend windows
- **Station clustering** — grouped stations by crime profile similarity
- **Temporal features** — year-over-year change rates

### 3. Ensemble modelling
Three models were trained and combined into a weighted ensemble:

| Model | Strength |
|---|---|
| Random Forest | Captures non-linear station-level patterns |
| XGBoost | Handles structured tabular data with high accuracy |
| LightGBM | Fast training on large datasets with strong generalisation |

Ensemble predictions outperformed any single model by leveraging each model's complementary strengths.

### 4. Evaluation
- **MAE ~200 crimes per station-year** — strong accuracy for annual forecasting
- Precision, recall, and F1 used for high-risk classification (top 20% stations)
- Cross-validated across time splits to prevent data leakage

### 5. Geospatial & reporting
- Provincial-level crime maps generated using `gadm41_ZAF_1.json` boundary data
- Power BI dashboard built for stakeholder reporting and station-level drill-down

---

## Repository Structure

```
saps_crime_project/
├── data/                   # Raw and processed SAPS crime data
├── notebooks/              # Jupyter notebooks (EDA, modelling, forecasting)
├── models/                 # Saved trained models
├── sql/                    # SQL scripts for data extraction and aggregation
├── power bi/               # Power BI dashboard file (.pbix)
├── map_files/
│   └── gadm41_ZAF_1.json  # South Africa provincial boundary GeoJSON
└── SAPS_Theme.json         # Custom Power BI theme
```

---

## How to Run

```bash
# Clone the repository
git clone https://github.com/Toni8/saps_crime_project.git
cd saps_crime_project

# Install dependencies
pip install pandas numpy scikit-learn xgboost lightgbm matplotlib seaborn jupyter

# Launch notebooks
jupyter notebook notebooks/
```

Open the notebooks in order — EDA first, then feature engineering, then modelling.

---

## Tech Stack

`Python` · `Pandas` · `NumPy` · `Scikit-Learn` · `XGBoost` · `LightGBM` · `SQL` · `Power BI` · `Matplotlib` · `Seaborn` · `GeoJSON`

---

## About the Data

Data sourced from publicly available **SAPS (South African Police Service)** crime statistics, covering station-level crime counts across all provinces from 2008 to 2023. No personally identifiable information is included.

---

*Built by [Sihle Kalolo](https://github.com/Toni8) · [Portfolio](https://sihle-kalolo-portfolio.vercel.app/)*
