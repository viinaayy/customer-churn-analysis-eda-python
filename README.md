# 📉 Telecom Customer Churn Analysis — Exploratory Data Analysis

> **Author:** Vinay &nbsp;|&nbsp; **Domain:** Telecom &nbsp;|&nbsp; **Type:** Exploratory Data Analysis (EDA) &nbsp;|&nbsp; **Status:** Complete

---

## 📋 Brief Summary

This project performs a full-scale **Exploratory Data Analysis (EDA)** on a telecom customer churn dataset of ~440,000 records. The goal is to identify which customer segments are most at risk of churning and which behavioural signals are the strongest predictors — translating data patterns into concrete, business-actionable retention strategies.

---

## 🗂️ Table of Contents

1. [Overview](#overview)
2. [Problem Statement](#problem-statement)
3. [Dataset](#dataset)
4. [Tools & Technologies](#tools--technologies)
5. [Methods](#methods)
6. [Key Insights & Output](#key-insights--output)
7. [How to Run This Project](#how-to-run-this-project)
8. [Results & Conclusion](#results--conclusion)

---

## 🔭 Overview

Customer churn is one of the most critical and costly challenges facing telecom companies. This project takes a structured, end-to-end EDA approach — from raw data ingestion through cleaning, feature engineering, univariate and bivariate exploration, to correlation analysis — and frames every finding around a concrete business question.

The analysis is built to serve two audiences simultaneously:

- **Business stakeholders** — actionable retention triggers, risk segments, and prioritised intervention levers
- **Data science teams** — a clean, reproducible analytical foundation ready to feed into a predictive modelling pipeline

The notebook follows a professional structure with numbered sections, a Table of Contents, a consistent colour palette, and annotated visualisations throughout.

---

## ❓ Problem Statement

A telecom company is experiencing alarmingly high customer attrition. With an observed churn rate of **~56.7%** — well above the industry average — more than half of all customers are leaving. Given that acquiring a new customer costs **5–7× more** than retaining an existing one, even modest improvements in retention translate directly to significant revenue recovery.

**Key questions this analysis answers:**

| # | Question |
|---|----------|
| 1 | How severe is the churn problem — what fraction of customers are leaving? |
| 2 | Are there demographic patterns — does age or gender correlate with churn? |
| 3 | Do contract type and subscription tier significantly affect churn rates? |
| 4 | Which numeric features differ most between churned and retained customers? |
| 5 | How do all features correlate with each other and with the churn target? |

---

## 📊 Dataset

| Property | Detail |
|----------|--------|
| **Source** | [Telecom Customer Churn Dataset — Kaggle](https://www.kaggle.com/) |
| **Training set** | ~440,000 rows |
| **Test set** | ~64,000 rows |
| **Target variable** | `Churn` — binary flag (0 = Retained, 1 = Churned) |
| **Total features** | 11 (before engineering) |

### Feature Descriptions

| Feature | Type | Description |
|---------|------|-------------|
| `Age` | Numeric | Customer age in years |
| `Gender` | Categorical | Male / Female |
| `Tenure` | Numeric | Months as a customer |
| `Usage Frequency` | Numeric | Average monthly service usage count |
| `Support Calls` | Numeric | Number of support calls made |
| `Payment Delay` | Numeric | Average days payment is delayed |
| `Subscription Type` | Categorical | Basic / Standard / Premium |
| `Contract Length` | Categorical | Monthly / Quarterly / Annual |
| `Total Spend` | Numeric | Total spend to date (USD) |
| `Last Interaction` | Numeric | Days since last interaction with company |
| `Churn` | Binary (target) | 0 = Retained, 1 = Churned |

### Engineered Features

| Feature | Logic | Purpose |
|---------|-------|---------|
| `Tenure Group` | `pd.cut(Tenure, bins=[0,12,24,36,48,60,72])` | Human-readable yearly cohorts |
| `Age Group` | `pd.cut(Age, bins=[18,25,35,45,55,65,100])` | Age-band segmentation for bivariate analysis |
| `Churn Label` | `{0: 'Retained', 1: 'Churned'}` | Readable axis labels on visualisations |

---

## 🛠️ Tools & Technologies

| Tool | Version | Purpose |
|------|---------|---------|
| **Python** | 3.10+ | Core programming language |
| **pandas** | 1.5+ | Data loading, cleaning, and aggregation |
| **NumPy** | 1.23+ | Numeric operations, array masking for heatmap |
| **Matplotlib** | 3.6+ | Base plotting, bar charts, pie charts, annotations |
| **Seaborn** | 0.12+ | Statistical plots — KDE, heatmap, boxplot, countplot |
| **Jupyter Notebook** | 6.5+ | Interactive analysis and narrative environment |

---

## 🔬 Methods

### 1. Data Cleaning

- **Missing value detection** — visualised missing % per column; dropped rows where `< 0.5%` records had nulls (safe to drop given dataset size)
- **Dtype correction** — converted float columns to `int64` where appropriate (counts, binary flags)
- **Feature engineering** — binned `Tenure` into 6 yearly cohorts and `Age` into 6 age bands for bivariate breakdown

### 2. Univariate Analysis

Examined each variable in isolation to understand baseline distributions:

- **Churn rate** — pie chart with precise labelling
- **Age** — histogram with KDE overlay
- **Categorical features** — countplots for Gender, Subscription Type, Contract Length

### 3. Bivariate Analysis — Churn vs Features

Compared churn rates across all categorical and numeric dimensions:

- **Bar charts** — churn rate by Contract Length, Subscription Type, Tenure Group, Gender (with 50% reference line and percentage labels)
- **KDE + bar dual panel** — age distribution split by churn status, plus churn rate by age group
- **Box plots** — side-by-side distributions of all 7 numeric features for Retained vs Churned customers

### 4. Correlation Analysis

- **Pearson correlation heatmap** — full numeric feature correlation matrix
- **Ranked bar chart** — features sorted by absolute correlation with `Churn` for immediate readability

---

## 💡 Key Insights & Output

### Churn Rate Overview

> **56.7% overall churn** — more than 1 in 2 customers is leaving.

---

### Feature Ranking by Correlation with Churn

| Rank | Feature | Pearson r | Direction |
|------|---------|-----------|-----------|
| 1 | Support Calls | +0.55 | More calls → higher churn |
| 2 | Payment Delay | +0.49 | Longer delay → higher churn |
| 3 | Last Interaction | +0.31 | Less recent contact → higher churn |
| 4 | Total Spend | −0.17 | Higher spend → slightly lower churn |
| 5 | Tenure | −0.14 | Longer tenure → slightly lower churn |
| 6 | Age | ~0.00 | No meaningful linear relationship |
| 7 | Usage Frequency | ~0.00 | No meaningful linear relationship |

---

### Bivariate Highlights

**Contract Length** — the most impactful categorical feature:

| Contract Type | Churn Rate |
|---------------|-----------|
| Monthly | ~88% |
| Quarterly | ~55% |
| Annual | ~27% |

> Monthly customers churn at **3× the rate** of annual customers.

**Tenure Group** — churn is highest in the first year:

| Tenure Group | Churn Rate |
|--------------|-----------|
| 0–1 Year | ~73% |
| 1–2 Years | ~56% |
| 2–3 Years | ~46% |
| 3–4 Years | ~49% |
| 4–5 Years | ~58% |
| 5–6 Years | ~62% |

> Non-linear U-shape — early months and long-tenured customers are both high risk.

**Gender** — near-zero difference (~50/50 split, similar churn rates across both).

**Subscription Type** — all three tiers (Basic, Standard, Premium) show similar churn patterns.

---

## ▶️ How to Run This Project

### Prerequisites

- Python 3.10 or higher
- pip

### Step-by-step

**1. Clone the repository**
```bash
git clone https://github.com/your-username/telecom-churn-eda.git
cd telecom-churn-eda
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows
```

**3. Install all dependencies**
```bash
pip install -r requirements.txt
```

**4. Launch Jupyter Notebook**
```bash
jupyter notebook customer_churn_eda.ipynb
```

**5. Run the full analysis**

In the Jupyter toolbar: `Kernel → Restart & Run All`

> ⚠️ **Important:** Both CSV files must be in the **same directory** as the notebook before running:
> - `customer_churn_dataset-training-master.csv`
> - `customer_churn_dataset-testing-master.csv`

### Project Structure

```
telecom-churn-eda/
│
├── customer_churn_eda.ipynb                   # Main analysis notebook
├── customer_churn_dataset-training-master.csv # Training data (~440K rows)
├── customer_churn_dataset-testing-master.csv  # Test data (~64K rows)
├── requirements.txt                           # Python dependencies
└── README.md                                  # This file
```

---

## 📝 Results & Conclusion

### Summary of Findings

This EDA confirmed that customer churn in this telecom dataset is driven by a small number of high-signal features — not broad demographic factors. The key results:

| Finding | Insight | Recommended Action |
|---------|---------|-------------------|
| 56.7% overall churn | Systemic retention problem — not isolated | Company-wide retention initiative needed |
| Monthly contracts → 88% churn | Contract length is the #1 lever | Incentivise annual upgrades at onboarding |
| Support calls are the top numeric predictor | Unresolved frustration drives exit | Proactive outreach after 3+ support calls |
| Payment delay >15 days correlates with churn | Financial stress precedes exit | Trigger retention offer at the 15-day mark |
| 0–1 year cohort has highest churn (73%) | Onboarding experience is critical | Structured 90-day and 6-month check-ins |
| Gender has near-zero churn impact | No need to gender-segment retention | Redirect segmentation budget to contract/tenure |
| Spend & usage don't predict churn | Price alone won't fix retention | Focus on service quality, not discounting |

### What This Analysis Does Not Do

This is an EDA — it identifies **patterns and associations**, not causation. The test set target was intentionally withheld throughout to prevent data leakage. All insights are drawn from the training set only.

### Next Steps — Towards Predictive Modelling

| Step | Detail |
|------|--------|
| **Feature engineering** | Encode categoricals, add `Payment Delay > 15 days` binary flag, interaction terms (`Support Calls × Tenure`) |
| **Baseline model** | Logistic Regression — interpretable, fast, good benchmark |
| **Ensemble model** | XGBoost with cross-validation, tuned with Optuna |
| **Evaluation** | ROC-AUC, Precision-Recall curve, confusion matrix at business-appropriate threshold |
| **Business output** | Translate churn probability scores into expected revenue saved per retained customer |

---

## 👤 Author

**Vinay**
B.Tech Computer Science, NIMS University (2024)
Actively seeking Data Analyst roles — open to remote and on-site opportunities across India.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/vinay-sagar-b33a84145)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-181717?logo=github&logoColor=white)](https://github.com/your-viinaayy)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
