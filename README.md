# Climate-Change-and-Agricultural-Yield-Turkey

## *Project Idea*

This project aims to explore the relationship between **climate change variables** (temperature and precipitation) and **agricultural crop yield** across Türkiye’s regions.  
The hypothesis is that provinces or regions experiencing higher average temperatures and lower precipitation over time will exhibit **decreased crop productivity** (kg per decare).  

By combining historical meteorological data from the Turkish State Meteorological Service (MGM) with crop yield statistics from the Turkish Statistical Institute (TÜİK), the project will identify whether changes in climate indicators are statistically correlated with agricultural performance — and if certain crops (wheat, barley, corn, cotton, etc.) are more sensitive to climate fluctuations.

---

## *Description of Dataset*

The project will utilize two primary datasets:

### *Agricultural Production Dataset (Yield Statistics)*  
- **Source:** https://data.tuik.gov.tr/  
- **Coverage:** Annual crop yield (kg/decare) for key crops such as wheat, barley, corn, cotton, sunflower, etc.  
- **Geographical Unit:** Province or NUTS-2 regional level (to be aggregated into 7 regions if needed)  
- **Temporal Range:** 2005 – 2024  
- **Variables:**  
  - Crop type  
  - Region/Province code  
  - Year  
  - Yield (kg/decare)  

### *Meteorological Dataset (Climate Indicators)*  
- **Source:** https://www.mgm.gov.tr/veridegerlendirme/il-ve-ilceler-istatistik.aspx  
- **Coverage:** Monthly or annual average temperature (°C) and total precipitation (mm) per province  
- **Temporal Range:** 2005 – 2024  
- **Variables:**  
  - Province name  
  - Average temperature  
  - Total precipitation  
  - Year  

---

## *Plan*

### *Data Collection*
- **Agricultural Data Sources:**  
  - TÜİK Open Data Portal → “Bitkisel Üretim İstatistikleri” tables  
  - Data cleaning and transformation into time-series per crop  

- **Climate Data Sources:**  
  - MGM “İl ve İlçeler İstatistikleri” for temperature and rainfall  
  - Aggregation from monthly → annual averages per province  

---

### *Data Analysis Approach*

1. **Exploratory Data Analysis (EDA)**  
   - Visualize yearly trends of temperature, rainfall, and crop yield  
   - Map spatial patterns of average yield vs. climate conditions  
   - Identify outlier years (extreme droughts, heatwaves, etc.)  

2. **Statistical Analysis**  
   - Compute correlation matrices between temperature, rainfall, and yields  
   - Build regression models (e.g., OLS or multiple linear regression)  
     `Yield = β₀ + β₁*Temperature + β₂*Rainfall + ε`  
   - Test lagged effects (e.g., prior year rainfall impact on next year’s yield)  

3. **Visualization and Presentation**  
   - Time-series line charts for yield vs. climate per crop  
   - Heatmaps showing correlation strength per region and crop type  
   - Interactive maps (optional) of average yield changes over years  

---

### *Tools and Technologies*
- **Python:** Main analysis language  
- **Pandas & NumPy:** Data wrangling and aggregation  
- **Matplotlib & Seaborn:** Visualization and trend analysis  
- **Statsmodels / Scikit-learn:** Regression and correlation modeling  
- **Jupyter Notebooks:** For structured and reproducible workflow  
- **GeoPandas (optional):** For regional mapping visualizations  

---

## *Expected Outcomes*
- Quantitative assessment of how temperature and precipitation variations impact crop yield  
- Identification of crops most sensitive to heat or rainfall reduction  
- Regional insights into climate vulnerability of agriculture  
- Policy-relevant findings on where adaptive strategies (irrigation, drought-resistant crops) are most needed  
- Foundation for predictive models linking climate change indicators to future yield projections  

---

## *Potential Challenges*
- Missing or inconsistent data across provinces or years  
- Different measurement units or update frequencies between MGM and TÜİK  
- Confounding variables (soil quality, irrigation, fertilizer use, etc.)  
- Possible non-linear relationships requiring advanced modeling  
- Data access restrictions for older years or specific crops  

---

This project will provide empirical evidence on **how climate variability affects agricultural productivity in Türkiye**, supporting efforts toward sustainable agriculture and climate adaptation policy-making.

---
