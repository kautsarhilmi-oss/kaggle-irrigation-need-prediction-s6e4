# 🌾 Irrigation Need Prediction — Kaggle PS S6E4

[![Kaggle](https://img.shields.io/badge/Kaggle-Playground%20S6E4-blue)](https://www.kaggle.com/competitions/playground-series-s6e4)
[![Python](https://img.shields.io/badge/Python-3.10%2B-green)](https://python.org)
[![Score](https://img.shields.io/badge/Accuracy-0.9828-brightgreen)]()

## Overview

Multiclass classification to predict the level of irrigation need
(Low / Medium / High) for agricultural fields based on soil properties,
weather conditions, crop type, and farming practices.

- **Competition:** Kaggle Playground Series Season 6, Episode 4
- **Metric:** Accuracy & Macro F1
- **CV Accuracy:** 0.9828 | **CV Macro F1:** 0.9623
- **Model:** HistGradientBoostingClassifier (scikit-learn)

---

## Dataset

| Split | Rows    | Features | Notes                              |
|-------|---------|----------|------------------------------------|
| Train | 630,000 | 20       | Low 58.7% / Medium 37.9% / High 3.3% |
| Test  | 270,000 | 19       | No target label                    |

**Key challenge:** Multiclass imbalance — "High" irrigation need
only 3.3% of cases.

---

## Feature Engineering (10 new features)

| Feature | Rationale |
|---------|-----------|
| `water_stress` | Temperature / Rainfall ratio — core drought signal |
| `moisture_deficit` | Temperature minus soil moisture — evaporation pressure |
| `evapotranspiration` | (Temperature × Sunlight) / Humidity — crop water demand proxy |
| `wind_heat_index` | Wind speed × Temperature — drying effect |
| `soil_water_capacity` | Soil moisture × Organic carbon — water retention ability |
| `ph_moisture` | pH × Soil moisture interaction |
| `irrigation_per_area` | Previous irrigation normalized by field area |
| `rain_vs_prev_irrig` | Rainfall vs previous irrigation ratio |
| `heat_humidity` | Temperature × (1 - Humidity%) — perceived heat load |
| `mulching_bin` | Binary flag for mulching usage |

---

## Results

| Fold | Accuracy | Macro F1 |
|------|----------|----------|
| 1    | 0.98320  | 0.96395  |
| 2    | 0.98306  | 0.96306  |
| 3    | 0.98208  | 0.95993  |
| **Overall OOF** | **0.98278** | **0.96232** |

---

## Key Insights

- `water_stress` (Temperature/Rainfall) is the single strongest predictor
- Fields in "High" irrigation need show **temperature >35°C** with near-zero rainfall
- `Mulching_Used` significantly reduces irrigation need — captured via interaction features
- Season and Crop Growth Stage provide strong contextual signals

---

## How to Run

```bash
pip install scikit-learn pandas numpy scipy

# Download data from:
# https://www.kaggle.com/competitions/playground-series-s6e4/data
python irrigation_need_prediction.py
```

---

## Author

**Kautsar Hilmi** — Magister Teknik Informatika, Universitas Pamulang
*Data Science | Machine Learning | Analytics*

[![GitHub](https://img.shields.io/badge/GitHub-kautsarhilmi--oss-black)](https://github.com/kautsarhilmi-oss)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-kautsarhilmi-blue)](https://www.linkedin.com/in/kautsarhilmi/)
