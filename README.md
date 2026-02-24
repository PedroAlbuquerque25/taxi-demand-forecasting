# 🚖 Sweet Lift Taxi - Hourly Demand Forecasting

## 📌 Business Problem
Sweet Lift Taxi collected historical airport taxi order data. To attract more drivers during peak hours and reduce passenger wait times, the company needs to **predict taxi demand for the next hour**.

## 🎯 Objective
Build a time series forecasting model capable of predicting hourly taxi demand.

### Requirements:
* **Resample** data to hourly frequency.
* **Perform** feature engineering (Lags, Rolling windows, Calendar).
* **Train** multiple models with hyperparameter tuning.
* **Evaluate** using RMSE (Target: **RMSE ≤ 48** on the test set).

## 📂 Dataset
* **File**: `taxi.csv`
* **Target variable**: `num_orders`
* **Time granularity (raw)**: 10 minutes
* **Model granularity**: Hourly

## 🧠 Project Workflow

1.  **Data Preparation**: Parsed datetime index, sorted chronologically, resampled to hourly demand, and handled missing values using forward-fill.
2.  **Trend Analysis**: Verified chronological integrity and identified a clear growth trend in demand by comparing first vs. second half averages.
3.  **Feature Engineering**:
    * **Lag Features**: Captures short-term autocorrelation (Previous 24h + same hour last week/lag_168).
    * **Rolling Statistics**: Captures recent momentum (3, 6, and 12-hour windows).
    * **Calendar Features**: Hour of day, Day of week, Weekend indicator, and Friday indicator.

## 🤖 Models Evaluated
We utilized **TimeSeriesSplit (5 folds)** for validation to prevent data leakage and simulate real-world forecasting.

| Model | Purpose |
| :--- | :--- |
| **Linear Regression** | Baseline & interpretable model |
| **Random Forest** | Nonlinear pattern detection |
| **Gradient Boosting** | Boosted ensemble learning |

## 📊 Model Performance

| Model | RMSE | MAE | Train Time |
| :--- | :--- | :--- | :--- |
| **Linear Regression** | **34.82** | **25.68** | **~0.01s** |
| Gradient Boosting | 40.19 | 27.36 | ~5s |
| Random Forest | 42.72 | 28.75 | ~12s |

> **Requirement satisfied**: RMSE ≤ 48.
> **🏆 Best Model**: Linear Regression.

### Why Linear Regression performed best?
* **Autocorrelation**: Demand is strongly linked to recent history, which LR captures efficiently via lags.
* **Generalization**: Lower variance compared to complex ensembles, reducing overfitting risk.
* **Linearity**: Feature engineering (lags) linearized the relationship between time and demand.

## 📈 Forecast: Next Hour Demand
Based on the most recent observed data, the model predicts:
**≈ 263 taxi orders** for the next hour.

## 💼 Business Impact
* ✅ **Better driver allocation** during peak hours.
* ✅ **Reduced passenger wait times**.
* ✅ **Increased service reliability and revenue**.

## ⚙️ Technologies Used
* **Python 3.13**
* **Pandas & NumPy** (Data Manipulation)
* **Scikit-learn** (Machine Learning & TimeSeriesSplit)
* **Matplotlib** (Visualization)

## ▶️ How to Run
1.  **Clone repository**:
    ```bash
    git clone <repo-url>
    cd sweet-lift-taxi
    ```
2.  **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the notebook**: Open `notebook.ipynb` and run all cells.

## 🔮 Future Improvements
* **Data**: Add weather conditions, flight schedules, and holidays.
* **Modeling**: Test SARIMA, Prophet, or Deep Learning (LSTM).
* **Ops**: Implement automated hourly predictions and drift monitoring.

---
**Author**: Pedro Albuquerque
*Data Analytics & Data Science*

---

## 🤝 Contact
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/phaa/)