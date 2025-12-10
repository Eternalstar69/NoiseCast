# Project Overview

This project analyzes and forecasts hourly environmental noise levels (A_Leq) collected by Dublin City Council throughout 2013.
The workflow includes data integration, cleaning, exploratory analysis, anomaly detection, clustering, and hybrid forecasting using SARIMA + LSTM to improve prediction accuracy for smart-city noise monitoring.

# Objectives

1. Understand long-term patterns of city noise

2. Analyze hourly/weekly/monthly seasonality

3. Detect unusually high-noise days

4. Cluster noise behavior patterns (Quiet / Moderate / Noisy hours)

5. Build an accurate predictive model for hourly noise levels

6. Support SDG11 — Sustainable Cities & Communities

# Dataset

Source: Dublin City Council Noise Monitoring (2013)

Records: ~105,000+ (5-minute interval readings)

Key Features:

A_Leq — Equivalent continuous sound level

A_L10, A_L95 — High/low percentile noise

C_Leq, C_L10, C_L95

Timestamp (datetime)

Data were consolidated from 365 daily CSV files into a master time-series dataset.

# Workflow & Methodology
**1. Preprocessing**

1.Merge 365 daily files

2.Parse datetime & convert numeric fields

3.Remove impossible values (e.g., negative dB)

4.Identify and remove multi-hour missing blocks

5.Interpolate small gaps

6.Resample to hourly data

7.Feature Engineering:

8.hour, weekday, month

9.rolling means (1h, 6h, 24h)

10.first difference (diff)

11.peak-noise flag (is_peak)

**2. Exploratory Data Analysis**

1.Daily / Weekly / Monthly seasonality

2.Weekday vs Weekend comparisons

3.Peak noise hours (17:00–22:00)

4.Z-score anomaly detection for abnormal days

5.Distribution + outlier detection

**3. Clustering Noise Behaviour**

1.Applied K-Means on hourly acoustic features (A_Leq, A_L10, A_L95)

2.Identified 3 interpretable clusters:

3.Quiet Hours

4.Moderate Hours

5.Noisy Hours

6.Useful for scheduling noise-control policies.

**4. Forecasting Models
SARIMA (Baseline Model)**

Captures trend and daily seasonality (24 hours)
Model:
``
SARIMA(2,1,2) × (1,1,1,24)
``


**RMSE ≈ 3.7**
#
**Hybrid SARIMA + LSTM (Final Model)**

Step 1: SARIMA forecasts hourly noise


Step 2: LSTM learns SARIMA residuals


Step 3: Final forecast = SARIMA + LSTM_correction

**Performance:**

SARIMA RMSE: 3.7

Hybrid RMSE: 2.6
→ ~30–40% improvement

# Key Insights

Strong hourly & weekly seasonality

Noise rises during commute and evening periods

Weekends consistently quieter than weekdays

Several abnormal noisy days detected via Z-score

Clustering reveals clear acoustic behavior patterns

Hybrid model significantly improves forecasting accuracy
→ Useful for real-time noise alert systems

# Technologies Used

Python, NumPy, Pandas

Matplotlib, Seaborn

Statsmodels (SARIMAX)

TensorFlow / Keras (LSTM)

Scikit-learn (Clustering, Scaling)

# How to Run

Install dependencies:


``
pip install -r requirements.txt
``

Open the notebook:

jupyter notebook


Run notebooks in order:
01_preprocessing → 02_eda → 03_clustering → 04_sarima → 05_lstm_residual → 06_hybrid_forecast


# Outcome

The project provides both:

Actionable understanding of city noise dynamics

A high-accuracy hybrid forecasting model suitable for real-time urban noise management systems

Supports long-term planning, noise regulation, and smart-city monitoring (SDG11).
