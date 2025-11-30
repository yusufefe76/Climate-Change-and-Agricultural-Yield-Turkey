# Analysis of Global Happiness and Economic Freedom

## Project Idea  

This project investigates the relationship between a nation's **happiness level** and its **economic freedom**.  
Instead of relying only on GDP as a proxy for well-being, the project focuses on structural economic factors—such as **Property Rights**, **Business Freedom**, and **Government Integrity**—and examines how they relate to how happy people are in different countries.

By merging the *World Happiness Report* with the *Index of Economic Freedom*, the project aims to answer:

- Is there a statistically significant difference in **happiness rankings** between more free and less free economies?
- Which specific economic freedom factors (e.g., **Property Rights**, **Trade Freedom**) are most strongly associated with happiness?

---

## Description of Data

The analysis uses two primary datasets from Kaggle and focuses on the year **2019** to keep everything temporally consistent.

### 1. World Happiness Report (Primary Dataset)

- **Source:** Kaggle – `PromptCloudHQ/world-happiness-report-2019`  
- **Content:** Survey-based happiness rankings for countries around the world.  
- **Key Variables (after cleaning/renaming):**
  - `Country` – Country name (standardized).
  - `Happiness_Rank` – Rank of the country in the happiness report (1 = happiest).
  - Additional variables available in the raw dataset include: `GDP per capita`, `Social support`, `Healthy life expectancy`, etc. (not all are used yet in this version).

### 2. Economic Freedom Index (Enrichment Dataset)

- **Source:** Kaggle – `lewisduncan93/the-economic-freedom-index` (Heritage Foundation data)  
- **Content:** Scores of economic freedom based on rule of law, government size, regulatory efficiency, and openness of markets.  
- **Key Variables (after cleaning/renaming):**
  - `Country` – Country name (standardized).
  - `Year` – Year of the index (filtered to **2019**).
  - `Index Score` – Overall economic freedom score.
  - Sub-scores such as `Property Rights`, `Business Freedom`, `Tax Burden`, `Government Integrity`, etc. (to be used in later stages for deeper analysis).

### Enrichment & Merge

- Country names are standardized (e.g., `"Turkiye" → "Turkey"`, `"Korea, South" → "South Korea"`).
- The datasets are merged with an **inner join** on the `Country` column.
- The final merged dataset contains **≈145 countries**, each with both happiness rank and economic freedom metrics.

---

## Plan & Current Progress

### 1. Data Collection & Cleaning ✅

- Automated download via **`kagglehub`**.
- Multiple encodings handled (`UTF-8` vs `Latin-1`).
- Column names stripped of extra spaces and harmonized:
  - Examples: `Country (region)` / `Country or region` → `Country`  
    `Score` / `Ladder` → `Happiness_Rank`  
    `Name` / `Country Name` → `Country`  
    `Overall Score` → `Index Score`
- Duplicate columns removed after renaming.
- Filtered the economic freedom dataset to **Year = 2019** and merged via `Country`.

### 2. Exploratory Data Analysis (EDA) ✅

- Basic descriptive statistics for `Happiness_Rank` and `Index Score`.
- **Scatter plot**:
  - X-axis: `Index Score` (higher = more economically free).  
  - Y-axis: `Happiness_Rank` (lower rank = happier), with the Y-axis **inverted** so “better” ranks appear higher on the plot.
  - A regression line is added to visualize the trend.
- Planned/optional: correlation matrix and heatmaps between happiness and economic sub-scores (e.g., `Property Rights`, `Business Freedom`).

### 3. Hypothesis Testing ✅

- **Research Question:**  
  > Do countries with higher economic freedom have **better (lower)** happiness ranks than countries with lower economic freedom?

- **Grouping Strategy:**
  - Compute the median of `Index Score`.
  - Countries with `Index Score ≥ median` → **High Freedom Group**.
  - Countries with `Index Score < median` → **Low Freedom Group**.

- **Statistical Method:**
  - Two-sample **Welch t-test**  
    (`scipy.stats.ttest_ind(high_group, low_group, equal_var=False)`),  
    which does **not** assume equal variances between the groups.
  - Outcome variable: `Happiness_Rank` (lower rank = better/happier).

- **Key Result (example run):**
  - High Freedom Group: mean happiness rank ≈ **47** (better).  
  - Low Freedom Group: mean happiness rank ≈ **104** (worse).  
  - p-value is extremely small (p < 0.05, effectively ~0), so:
    - The null hypothesis (“no difference in happiness ranks between groups”) is **rejected**.
    - Interpretation: **More economically free countries tend to rank significantly higher (happier) in the World Happiness Report.**

> Note: Since `Happiness_Rank` is an ordinal rank, non-parametric alternatives such as the Mann–Whitney U test could also be considered in future extensions. For this version, the Welch t-test provides a clear and interpretable comparison.

### 4. Machine Learning & Deeper Analysis (Planned)

Planned for a later stage:

- **Regression Models**
  - Linear or regularized regression models predicting `Happiness_Rank` from economic freedom sub-scores (e.g., `Property Rights`, `Business Freedom`, `Tax Burden`, `Government Integrity`).
  - Interpretation of feature coefficients to see which dimensions of economic freedom are most associated with better happiness ranks.

- **Clustering**
  - K-Means clustering of countries using both economic and happiness variables.
  - Example clusters:  
    - “High Freedom / High Happiness”  
    - “High Freedom / Lower Happiness” (outliers)  
    - “Low Freedom / Low Happiness”, etc.

---

## Tools & Technologies

- **Data Manipulation:** `pandas`, `numpy`  
- **Data Ingestion:** `kagglehub`, `os`  
- **Visualization:** `seaborn`, `matplotlib`  
- **Statistical Analysis:** `scipy.stats` (Welch t-test, and possibly non-parametric tests in future work)  
- **Environment:** Spyder / Jupyter Notebook (Python 3.x)

---

## How to Run

### 1. Install Dependencies

```bash
pip install pandas numpy seaborn matplotlib scipy kagglehub
