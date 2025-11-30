# Analysis of Global Happiness and Economic Freedom

## *Project Idea*
This project aims to investigate the relationship between a nation's **happiness score** and its **economic/social indicators**. By merging the *World Happiness Report* with external economic datasets (such as the *Economic Freedom Index* or *World Bank Data*), I plan to determine which factors—beyond GDP—most significantly impact societal well-being.

The project will enrich the standard happiness data to explore questions like:
- Does higher economic freedom always correlate with higher happiness?
- Can we predict a country's happiness score based on its inflation and unemployment rates?

## *Description of Data*

The project will utilize two primary datasets sourced from Kaggle to satisfy the enrichment requirement:

### *1. World Happiness Report (Primary Dataset)*
- **Source:** Kaggle (World Happiness Report 2015-2024)
- **Content:** Happiness scores, GDP per capita, Social support, Healthy life expectancy, Freedom to make life choices.
- **Key Variables:** `Country`, `Year`, `Ladder Score (Happiness)`, `Log GDP per capita`.

### *2. Economic Freedom Index / World Indicators (Enrichment Dataset)*
- **Source:** Kaggle (Economic Freedom Index)
- **Content:** Trade freedom, Tax burden, Government spending, Inflation rates, Unemployment.
- **Enrichment Plan:** This dataset will be merged with the Happiness Report using `Country` and `Year` keys to analyze the impact of specific economic policies on happiness.

---

## *Plan*

### *Data Collection & Cleaning (Deadline: Nov 28)*
- Download datasets from Kaggle.
- Standardize country names (e.g., matching "USA" in one file to "United States" in the other).
- Merge datasets into a single Pandas DataFrame.
- Handle missing values (imputation or removal).

### *Exploratory Data Analysis (Deadline: Nov 28)*
- **Visualizations:**
  - Heatmaps showing correlations between Happiness and Economic Freedom.
  - Choropleth maps visualizing global happiness distribution.
  - Scatter plots: Inflation vs. Happiness.
- **Hypothesis Testing:**
  - Test if countries with high "Economic Freedom" have statistically higher happiness scores compared to those with low freedom.

### *Machine Learning Models (Deadline: Jan 02)*
- **Regression Analysis:** Build models (Linear Regression, Decision Trees) to predict the `Happiness Score` using features like Tax Burden, Inflation, and GDP.
- **Clustering:** Use K-Means to group countries into clusters (e.g., "Sad but Wealthy", "Happy and Free") to find hidden patterns.

---

## *Tools*
- **Python:** Pandas, NumPy for data manipulation.
- **Visualization:** Matplotlib, Seaborn, Plotly (for maps).
- **Machine Learning:** Scikit-learn.
