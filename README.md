# **Time-Series Forecasting of Urban Mobility Patterns in Public Transport Data**

**Why ARIMA Fits This Dataset**
**Clear Autocorrelation Patterns Identified During EDA**

From the cross-correlation and autocorrelation plots, it was evident that:

Yesterday’s ridership strongly influences today’s ridership.

The dataset exhibits lag-based dependencies typical in commuter data.

ARIMA is specifically designed to model autocorrelation using the autoregressive (AR) and moving average (MA) components.

**The Dataset Shows Mild Non-Stationarity**

The rolling mean and rolling variance plots show:

Slight upward or downward drifts over long periods

Local fluctuations around a baseline pattern

ARIMA handles this using the Integrated (I) component, which applies differencing to stabilize the mean.

This makes ARIMA ideal for your dataset because:

It stabilizes trends

Removes long-term drifts

Makes the series suitable for forecasting

**ARIMA Works Extremely Well for Univariate Time-Series**

Each service in your dataset (Local Route, Rapid Route, Light Rail, etc.) is a single-column time series.

ARIMA excels in univariate forecasting scenarios because:

It doesn't require additional features

It models temporal patterns directly

It performs accurately even with small datasets

Given your data format, ARIMA is the best-fitting classical model.

**ARIMA Provides Highly Interpretable Statistical Structure**

ARIMA produces interpretable parameters:

p → autoregressive terms

d → differencing

q → moving average terms

These help you understand:

How many past days influence the forecast

Whether the series needed differencing

How noise affects the system

This interpretability is extremely useful in a real-world transportation context.

**ARIMA Is Efficient and Fast**

Your dataset has ~1900 daily observations — small enough that ARIMA trains in:

1–3 seconds for model fitting

Instantly for forecasting

In contrast, LSTMs or Prophet models require more compute and tuning.

**Forecasting**


![Future Forecast](/future_forecast.jpeg)

# **1. Strong Weekly Seasonality Dominates Ridership Trends**
STL decomposition shows that weekly seasonality contributes more variance than long-term trends. This stable, recurring weekly pattern makes the dataset highly suitable for models like Prophet and SARIMA.
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
