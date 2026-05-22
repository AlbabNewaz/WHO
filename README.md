# WHO Mortality Data Analysis
### Exploring Gender Disparities and Economic Indicators in Global Healthcare

**Course:** DSC207 — Introduction to Data Science  
**Dataset:** [WHO Mortality Database](https://www.who.int/data/data-collection-tools/who-mortality-database)  
**Language:** Python · Jupyter Notebook

---

## Overview

This project analyzes the WHO Mortality Database to investigate how economic indicators relate to healthcare quality across countries — and whether disparities in male vs. female mortality outcomes grow or shrink as healthcare improves.

A custom age-weighted scoring system was developed to assign a single healthcare score to each country and sex, enabling cross-country comparison. The score heavily penalizes child and early-age mortality while rewarding deaths at older ages, reflecting the idea that a higher-quality healthcare system keeps people alive longer.

---

## Research Questions

**Q1 — Gender Discrepancy vs. Healthcare Score**  
Do countries with higher overall healthcare scores show a larger or smaller gap between male and female mortality scores?

**Q2 — Purchasing Power Parity vs. Median Income as Predictors**  
Between GDP (PPP-adjusted) and median income, which is the better economic predictor of a country's healthcare score?

**Q3 — GDP per Capita vs. Healthcare Score (2018, pre-COVID)**  
Is there a strong correlation between GDP and health outcomes? And are there notable outliers — high-GDP countries with surprisingly low scores, or vice versa?

---

## Methodology

### Scoring System

Each country is assigned a healthcare score based on deaths per 100,000 population, weighted by age group. The multipliers range from **−3** (infant mortality) to **+3** (deaths at 85+), reflecting the principle that deaths at older ages indicate a healthier population overall:

| Age Group | Multiplier |
|-----------|------------|
| [0]       | −3.0       |
| [1–4]     | −2.0       |
| [5–9]     | −1.5       |
| [10–14]   | −1.0       |
| [15–19]   | 0.0        |
| [20–24]   | +0.5       |
| ...       | ...        |
| [80–84]   | +2.6       |
| [85+]     | +3.0       |

Scores are computed separately for **Male**, **Female**, and **All**, then aggregated per country. The Male–Female score difference is used as the **discrepancy metric**.

### Data Sources

| Data | Source |
|------|--------|
| WHO Mortality Dataset | Google Sheets (custom export) |
| GDP per capita (2018) | [Our World in Data — Maddison Project](https://ourworldindata.org/grapher/gdp-per-capita-maddison) |
| Median Income by Country | [World Population Review](https://worldpopulationreview.com/country-rankings/median-income-by-country) |
| GDP (PPP-adjusted) | World Population Review |

---

## Key Findings

**Q1 — Gender Discrepancy:**  
Contrary to the initial hypothesis, countries with *higher* overall healthcare scores tend to have a *larger* male–female discrepancy. This suggests that as healthcare quality improves, women may benefit proportionally less than men — an unexpected and thought-provoking result. Note that the dataset does not capture maternal mortality during childbirth, which may partially explain this gap.

**Q2 — PPP vs. Median Income:**  
Both GDP (PPP-adjusted) and median income correlate strongly with healthcare scores. Visually the scatter plots are nearly identical, but GDP (PPP) yields a stronger correlation coefficient, making it the marginally better economic predictor of healthcare outcomes.

**Q3 — GDP vs. Healthcare Score:**  
There is a strong overall correlation between GDP per capita and healthcare scores. Notably, *no* country in the dataset had a high healthcare score alongside low GDP — consistent with the intuition that financial resources underpin healthcare capacity.

The most interesting outliers were countries with *high GDP but low healthcare scores*, all of which came from the **Middle East**. While the dataset alone cannot confirm causation, this pattern is consistent with known wealth inequality in the region, where high aggregate production does not translate to broad population health outcomes.

---

## Project Structure

```
WHO/
├── WHO_mortality_dataset_project.ipynb   # Full analysis notebook
└── README.md
```

---

## Getting Started

### Prerequisites

```
pandas
numpy
matplotlib
seaborn
scikit-learn
tabulate
```

Install with:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn tabulate
```

### Running the Notebook

```bash
git clone https://github.com/AlbabNewaz/WHO.git
cd WHO
jupyter notebook WHO_mortality_dataset_project.ipynb
```

> **Note:** The notebook loads data directly from Google Sheets via URL. An active internet connection is required to reproduce the analysis.

---

## Limitations

- The age-weighted scoring system is arbitrary and not validated against established healthcare indices.
- Maternal mortality during childbirth is not explicitly tracked in the dataset, which may affect the gender discrepancy findings.
- GDP and income data are from 2018 (pre-COVID) and may not reflect current conditions.
- Country name matching across datasets may result in some records being dropped during merges.

---

## Acknowledgements

Data sourced from the [WHO Mortality Database](https://www.who.int/data/data-collection-tools/who-mortality-database), Our World in Data, and World Population Review. This project was completed as a final project for DSC207.
