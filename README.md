# Global Happiness & Economic Freedom (2019) — Statistical Testing + ML

This project analyzes how a country’s **happiness** relates to its **economic freedom** in **2019**, using the *World Happiness Report* and the *Index of Economic Freedom*. Beyond GDP alone, the analysis focuses on structural freedom dimensions like **Property Rights**, **Business Freedom**, and **Government Integrity**, and evaluates both statistical differences and predictive power.

---

## Data Sources (2019)

All analysis is restricted to **2019** to keep the datasets temporally consistent.

1) **World Happiness Report 2019** (Kaggle)  
- Dataset: `PromptCloudHQ/world-happiness-report-2019`  
- Key fields used:
  - `Country`
  - `Happiness_Rank` (ordinal: 1 = happiest)
  - `Happiness_Score` (continuous: higher = happier)
  - Optional WHR components (if included): `GDP per capita`, `Social support`, `Healthy life expectancy`, etc.

2) **Index of Economic Freedom** (Heritage Foundation / Kaggle)  
- Dataset: `lewisduncan93/the-economic-freedom-index`  
- Key fields used:
  - `Country`, `Year` (filtered to 2019)
  - `Index_Score` (overall freedom score)
  - Sub-scores such as `Property Rights`, `Business Freedom`, `Government Integrity`, `Trade Freedom`, etc.

> Notes on correctness: `Happiness_Score` is treated as the primary continuous outcome. `Happiness_Rank` is used as an ordinal robustness outcome.

---

## What This Repo Does

### 1) Data Cleaning & Merge
- Downloads data via `kagglehub`.
- Handles common encoding issues (UTF-8 vs Latin-1).
- Standardizes country names (e.g., `Turkiye → Turkey`, `Korea, South → South Korea`).
- Filters the Economic Freedom dataset to **Year = 2019**.
- Merges with an **inner join** on `Country`.
- Final merged dataset contains **~145 countries** with both happiness and freedom metrics.

### 2) Exploratory Data Analysis (EDA)
- Descriptive statistics for happiness and freedom variables.
- Visualizations:
  - `Index_Score` vs `Happiness_Score` (main relationship plot)
  - `Index_Score` vs `Happiness_Rank` (rank-based robustness; y-axis inverted so “happier” appears higher)
- Optional: correlation heatmaps between happiness outcomes and freedom sub-scores.

---

## Hypothesis Testing (Completed)

### Core Research Question
**Do countries with higher economic freedom have higher happiness (better rank / higher score) than countries with lower economic freedom?**

### Grouping Strategy
- Compute the median of `Index_Score`
- `Index_Score ≥ median` → **High Freedom**
- `Index_Score < median` → **Low Freedom**

### Statistical Tests
- **Welch Two-Sample t-test** (does not assume equal variances)
- **Mann–Whitney U** (non-parametric robustness; useful since ranks are ordinal)
- Effect size (Cohen’s d) reported for mean-based comparisons

### Key Finding (Observed)
Using `Happiness_Rank` as outcome:
- High Freedom group mean rank ≈ **47** (better/happier)
- Low Freedom group mean rank ≈ **104** (worse/less happy)
- p-value extremely small (p < 0.05), rejecting the null hypothesis  
**Conclusion:** More economically free countries tend to be significantly happier (as measured by 2019 happiness ranks).

### Extended Hypothesis Testing (Completed)
To move beyond the overall index:
- Repeat the same **High vs Low** comparisons for each freedom sub-score:
  - e.g., `Property Rights`, `Business Freedom`, `Government Integrity`, `Trade Freedom`, etc.
- Apply **multiple-comparison correction** (Holm or Benjamini–Hochberg FDR) to control false positives.
- Output: a results table with raw p-values, corrected p-values, and effect sizes for each metric.

---

## Machine Learning (Completed)

ML is used to answer the “which factors matter most?” question more directly and to test predictive strength.

### Targets
- Primary: `Happiness_Score` (regression; preferred because it is continuous)
- Secondary (optional): categorize happiness into groups (classification):
  - e.g., High vs Low happiness (median split) or Top/Bottom tercile

### Features
- Main feature set: Economic freedom metrics
  - Overall: `Index_Score`
  - Sub-scores: `Property Rights`, `Government Integrity`, `Business Freedom`, etc.
- Optional second feature set: include WHR components to compare explanatory power

### Models Trained
**Regression**
- Linear Regression (baseline)
- Ridge / Lasso / Elastic Net (handles correlated predictors; Lasso/Elastic Net adds feature selection)
- Random Forest Regressor (nonlinear, interaction-friendly)
- Gradient Boosting Regressor (strong tabular performance; captures nonlinear patterns)

**Classification (optional track)**
- Logistic Regression
- Random Forest / Gradient Boosting Classifier

### Validation & Metrics
Because the dataset is relatively small (~145 rows), evaluation emphasizes stability:
- **k-fold cross-validation** (typically 5-fold or 10-fold)
- Regression metrics:
  - MAE, RMSE, R²
- Classification metrics (if used):
  - Accuracy, F1, ROC-AUC
- Optional rank agreement:
  - Spearman correlation between predicted and true ranks (robust check)

### Interpretability (Completed)
To identify the freedom dimensions most associated with happiness:
- Linear models: standardized coefficients
- Tree models: permutation feature importance
- Optional: SHAP (if enabled) for local + global explanations

---

## Outputs
The pipeline produces:
- Clean merged dataset (2019)
- EDA figures (scatterplots + optional correlation heatmaps)
- Hypothesis testing tables:
  - overall index test
  - per-subscore tests with corrected p-values
- ML evaluation summaries (cross-validated metrics)
- Feature importance / interpretability outputs

---

## How to Run

### 1) Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn kagglehub
