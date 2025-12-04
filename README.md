# **Time-Series Forecasting of Urban Mobility Patterns in Public Transport Data**

**Why SARIMA Was Chosen**
**Strong Weekly Seasonality Identified**

Exploratory Data Analysis (STL decomposition and rolling mean plots) revealed a clear 7-day repeating pattern:

Higher ridership on weekdays

Significant drops on weekends

This pattern repeats consistently across years

ARIMA cannot model such repeating cycles, but SARIMA is specifically designed to capture seasonal patterns via the seasonal order terms:​

where m=7

This makes SARIMA the most appropriate statistical model for the dataset.

**Autocorrelation Exhibits Seasonal Lag Structure**

ACF plots show pronounced spikes at lag = 7, 14, 21…
This means ridership on a given day is strongly influenced by ridership from one week prior.

This kind of periodic autocorrelation is a textbook indicator for using a seasonal ARIMA model.

**Short-Term Dynamics + Seasonal Patterns**

The dataset shows:

Strong short-term autocorrelation (lags 1–3)

Weekly seasonal periodicity (lag 7)

Mild long-term trend

Occasional anomalies

SARIMA is uniquely equipped to combine:

Short-term AR/MA behavior (via p, q)

Differencing to remove trend (via d)

Seasonal differencing to remove weekly cycles (via D)

Seasonal AR/MA terms for weekly influence

This makes SARIMA superior to ARIMA, ETS, and simple exponential smoothing.

**Multivariate Features Are Not Required**

Each service (Local Route, Rapid Route, Peak Service, etc.) is forecasted individually.
SARIMA works well for univariate seasonal time series, making it a natural fit.

**SARIMA Model Configuration**​

Auto-ARIMA determined the best combination of parameters for each service:

p, d, q capture short-term autoregressive patterns

P, D, Q capture weekly seasonal influence

m = 7 because ridership follows a 7-day cycle

This ensures the model accounts for both day-to-day fluctuations and weekly commuting behavior.

**Model Training & Validation**
**Train–Test Split**

The final 30 days of the dataset were used as a validation window.

SARIMA forecasted those 30 days.

Actual vs forecast values show strong alignment.

**Forecast Confidence Intervals**

The model outputs a 95% confidence interval, showing uncertainty around predictions.
This is crucial for transport planning, where unexpected events may cause deviations.

**Diagnostic Checks**

SARIMA residual diagnostics indicate:

Residuals resemble white noise (no patterns left)

No strong autocorrelation in residuals

Variance is stable

Forecast errors centered around zero

This confirms the model successfully captured the meaningful structure of the series.

**Forecasting**


![Future Forecast](/future_forecast.jpeg)

# **1. Strong Weekly Seasonality Dominates Ridership Trends**
STL decomposition shows that weekly seasonality contributes more variance than long-term trends. This stable, recurring weekly pattern makes the dataset highly suitable for models like Prophet, SARIMA and ARIMA.
![STL Decomposition](/STL_decomposition.png)

# **2. Local Route Ridership Predicts Peak Service with a 1-Day Lead**
Cross-correlation reveals that Peak Service ridership strongly correlates with Local Route lagged by one day. This natural lead–lag relationship is valuable for building lag-based forecasting models.
![Cross Correlation](/cross_correlation.png)

# **KMeans Clustering Reveals Three Hidden “Day Types” Beyond Weekday/Weekend Patterns**
Unsupervised clustering identified three distinct types of days:

Cluster 1: High-demand commuter days

Cluster 2: Medium, transition-type days

Cluster 3: Low-demand days (holidays/weekends)

**Why this matters:**

Cluster labels can be added as features to the forecasting model.

Improves accuracy by accounting for structural day-type patterns.
![Cluster Analysis](/cluster_analysis.png)

# **4. Rapid Route to Local Route Ratio Remains Structurally Stable Over Time**

The ridership ratio Rapid Route / Local Route stays within a narrow range, even during major ridership changes.

**Why this matters:**

Indicates a stable behavioral relationship between service types.

You can create a powerful feature "Rapid_Local_Ratio"

Adds robustness to multi-output forecasting models.

# **5. Rolling Statistics Reveal Anomalies Not Explained by Weekends or Holidays**

The 7-day and 30-day rolling averages expose irregular drops that are not part of the weekly seasonal pattern.

**Why this matters:**

These anomalies may correspond to operational disruptions or unusual events.

They should be handled separately during model training (e.g., anomaly flags).
