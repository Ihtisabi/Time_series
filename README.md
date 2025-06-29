# Surface Temperature Forecasting in Indonesia
### CodingCamp DBS Foundation 2025 - Machine Learning Final Project

You can read the full report in [Laporan Proyek](laporan.md), however, the full report is currently only available in Indonesian.

## 🌏 Domain
This project focuses on **climate science**, particularly surface temperature trends as a key indicator of climate change. As a tropical archipelagic country, **Indonesia** is highly vulnerable to climate-related impacts such as sea level rise, heatwaves, and agricultural disruption.

## 🎯 Objectives
- Analyze long-term surface temperature trends in Indonesia (1940–2024).
- Perform seasonal analysis of monthly temperature patterns.
- Build predictive models using time series methods (ARIMA, AutoARIMA, Prophet).
- Evaluate models using error metrics: RMSE, MAE, MAPE, SMAPE.

## 📊 Dataset
- **Source**: Kaggle (original data from World Bank).
- **Data Period**: 1940–2024.
- **Granularity**: Monthly average surface temperature.
- **Country**: Filtered to **Indonesia** only.
- **Rows**: 1,020 (cleaned & processed).

[Dataset on Kaggle](https://www.kaggle.com/datasets/samithsachidanandan/average-monthly-surface-temperature-1940-2024)

## 🛠️ Models Used
| Model       | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| ARIMA       | Classical statistical model for linear, non-seasonal time series            |
| AutoARIMA   | Automatically selects optimal parameters (p,d,q) using AIC-based search     |
| Prophet     | Decomposes time series into trend + seasonality using Bayesian methods      |

## ✅ Results & Evaluation

| Model        | RMSE   | MAE    | MAPE   | SMAPE  |
|--------------|--------|--------|--------|--------|
| ARIMA (1,1,1)| 0.423  | 0.361  | 1.409% | 1.423% |
| AutoARIMA    | 0.423  | 0.361  | 1.409% | 1.423% |
| **Prophet**  | **0.195**  | **0.148**  | **0.580%** | **0.582%** |

> **Best Model:** Prophet (MAPE: 0.58%)  
> Prophet captured the seasonal and trend components of Indonesia's temperature data effectively.

## 🔧 Tuning Prophet
- Used manual grid search and cross-validation.
- Final MAPE after tuning: **0.618%**
- Original model was already highly optimized.

## 📈 Insights
- Indonesia shows a **gradual but significant warming trend** since the 1980s.
- Monthly fluctuations are mild due to the tropical climate (range ~0.6°C/year).
- Peak temperatures occur in **May and October**, lowest in **July**.

## 🧠 Key Takeaways
- Prophet is a powerful tool for modeling **mild seasonal** data with long-term trends.
- Forecasting surface temperature helps stakeholders develop data-driven **climate adaptation strategies**.
- Supports early warnings and mitigation planning for sectors like agriculture and public health.

---

_This project was developed as part of the **CodingCamp DBS Foundation 2025**, Machine Learning Track._
