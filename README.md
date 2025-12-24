# Global-Child-Mortality-Economic-Correlation-Analysis

## 📌 Project Overview
This project analyzes the relationship between national wealth (GDP per capita) and Child Mortality Rates (CMR) across 60+ years of global data. The goal was to determine if economic growth is the sole driver of child survival or if regional policies and health initiatives create "Success Stories" where countries outperform their economic status.

## 🛠️ The Data Pipeline
### Phase 1: Data Audit & Cleaning (Excel & Python)
* Audit: Using Excel, I identified that the raw dataset mixed individual country data with regional aggregates (e.g., "Africa", "World"), leading to double-counting in population metrics.

* **Cleaning**: Used **Python (Pandas)** to:

  * Remove rows with missing GDP or CMR values.

  * Eliminate impossible negative values and extreme 3-digit outliers.

  * Filter the dataset to include only entities with valid country codes to ensure analysis granularity.
 
### Phase 2: Relational Mapping (SQL)
* **The Challenge**: The original dataset was missing a dedicated "Region" column for many countries.

* **The Solution**: Imported the cleaned data into **MySQL** and performed a `LEFT JOIN` with a secondary continent mapping table.

* **Permanent View**: Created another table to serve as a "Single Source of Truth" for Power BI, ensuring that regional aggregates were excluded to prevent inflated population sums.

### Phase 3: Statistical Analysis (Python)
* **Correlation**: Generated a **Heatmap** which revealed a moderate **negative correlation of** $-0.48$ between GDP and CMR.

* **Distribution**: Developed **Box Plots** to visualize regional inequality, highlighting that while the global trend is declining, regions like Africa and the Americas show significant internal variance (outliers).

* **Implication**: The -0.48 correlation suggests that wealth explains only about 50% of child mortality outcomes, leaving significant room for healthcare policy impact.

### Phase 4: Data Visualization (Power BI)
Built an interactive dashboard featuring:

* **KPI Cards**: Displaying the exact World Population (~8.02 billion in 2022) using DAX measures to avoid historical summation.

* **Scatter Plot**: Visualizing the Wealth vs. Health correlation.

* **Area Chart**: Showing the longitudinal decline of CMR by region.

* **Top 6 Leaderboard**: Identifying countries with the highest and lowest current mortality rates.

## 📈 Key Insights
1. **Wealth is not Destiny**: Several "High-Performing" countries were identified that achieved lower-than-average mortality rates despite having lower-than-average GDP.

2. **Regional Disparity**: Oceania and the Amwricas show the tightest clusters of success, while Africa shows the widest gap between high and low-performing nations.

3. **Population Neutrality**: Statistical analysis showed a near-zero correlation (-0.02) between a country's total population and its mortality rate, debunking the idea that population size drives health outcomes.
