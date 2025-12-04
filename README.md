# **Time-Series Forecasting of Urban Mobility Patterns in Public Transport Data**

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
