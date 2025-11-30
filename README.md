# Analysis of Global Happiness and Economic Freedom

## *Project Idea*
This project aims to investigate the relationship between a nation's **happiness score** and its **economic freedom**. While GDP is often used as the primary proxy for well-being, this project hypothesizes that structural economic factors—such as **Property Rights**, **Business Freedom**, and **Government Integrity**—have a direct and significant correlation with a population's happiness.

By merging the *World Happiness Report* with the *Index of Economic Freedom*, I enrich the standard happiness data to answer:
- Is there a statistically significant difference in happiness between free and repressed economies?
- Which specific economic freedom factor (e.g., Trade Freedom vs. Property Rights) correlates most strongly with happiness?

---

## *Description of Data*

The project utilizes two primary datasets sourced from Kaggle to satisfy the enrichment requirement. The analysis focuses on the year **2019** to ensure temporal consistency between the two sources.

### *1. World Happiness Report (Primary Dataset)*
- **Source:** Kaggle (PromptCloudHQ/world-happiness-report-2019)
- **Content:** Survey data from 156 countries ranking their happiness levels.
- **Key Variables:** `Country`, `Happiness_Score` (Ladder), `GDP per capita`, `Social support`, `Healthy life expectancy`.

### *2. Economic Freedom Index (Enrichment Dataset)*
- **Source:** Kaggle (Heritage Foundation / lewisduncan93)
- **Content:** A comprehensive scoring of economic freedoms based on rule of law, government size, regulatory efficiency, and open markets.
- **Key Variables:** `Country`, `Index Score` (Overall), `Property Rights`, `Business Freedom`, `Tax Burden`, `Government Integrity`.
- **Enrichment Plan:** These datasets are merged using a standardized **`Country`** column to map economic policies directly to happiness outcomes.

---

## *Plan*

### *1. Data Collection & Cleaning (Completed)*
- **Ingestion:** Automated download using `kagglehub` API.
- **Encoding Handling:** Managed `Latin-1` vs `UTF-8` encoding issues common in country-level datasets.
- **Standardization:**
  - Standardized country names (e.g., mapping "Turkiye" to "Turkey", "USA" to "United States").
  - Handled column naming discrepancies (e.g., `Country (region)` vs `Country Name`).
- **Merging:** Successfully merged datasets via an inner join, resulting in a clean dataset of **~140+ countries**.

### *2. Exploratory Data Analysis (Completed)*
- **Correlation Matrix:** Computed Pearson correlations to identify strong relationships.
  - *Preliminary Finding:* `Property Rights` and `Index Score` showed strong positive correlations with Happiness.
- **Visualizations:**
  - **Heatmap:** To visualize the strength of relationships between economic sub-factors and happiness.
  - **Scatter Plots:** Plotted `Index Score` vs. `Happiness_Score` to observe the linear trend.

### *3. Hypothesis Testing (Completed)*
- **Hypothesis:** Countries with "High Economic Freedom" (above median) have higher happiness scores than those with "Low Economic Freedom".
- **Method:** Independent T-Test (Two-sample).
- **Result:** The T-Test yielded a **p-value < 0.05**, rejecting the null hypothesis. This statistically confirms that economic freedom is associated with higher happiness.

### *4. Machine Learning Models (Planned: Jan 02)*
- **Regression Analysis:** Build a Linear Regression model to predict a country's `Happiness Score` based on its specific economic freedom sub-scores (e.g., Property Rights, Tax Burden).
- **Clustering:** Use K-Means Clustering to group countries into categories such as "High Income/Low Happiness" vs. "Medium Income/High Happiness" to detect anomalies.

---

## *Tools & Technologies*
- **Data Manipulation:** `pandas`, `numpy`
- **Data Ingestion:** `kagglehub`, `os`
- **Visualization:** `seaborn`, `matplotlib`
- **Statistical Analysis:** `scipy.stats` (T-Tests)
- **Environment:** Spyder / Jupyter Notebook

---

## *How to Run*
1. Install dependencies:
   ```bash
   pip install pandas seaborn matplotlib scipy kagglehub
