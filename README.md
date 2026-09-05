# 🍷 Wine Reviews — Data Cleaning & Exploratory Data Analysis

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-Data%20Cleaning-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0" alt="Seaborn">
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen" alt="Status">
  <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License">
</p>

<p align="center">
  A clean, end-to-end exploration of the <b>Wine Reviews</b> dataset (130k+ reviews) — from raw CSV to
  polished, decision-ready visualizations on wine quality, variety, and price.
</p>

---

## 📖 Overview

This project takes the popular **[Wine Reviews dataset](https://www.kaggle.com/datasets/zynicide/wine-reviews)**
(`winemag-data-130k-v2.csv`) through a full data cleaning and exploratory data analysis (EDA) pipeline.
The goal is to answer a simple question with real evidence: **what drives a wine's rating, and how does
that relate to price and variety?**

The notebook covers:

- 🧹 **Cleaning** — dropping junk columns, removing duplicates, and handling missing values
- 🔍 **Exploration** — inspecting structure, types, and data quality
- 📊 **Visualization** — bar, box, violin, count, scatter, facet, and histogram plots to surface patterns
  across wine variety, points (ratings), and price

---

## 🗂️ Dataset

| Detail | Description |
|---|---|
| **Source** | Wine Enthusiast reviews, scraped and published on Kaggle |
| **File** | `winemag-data-130k-v2.csv` |
| **Size** | ~130,000 rows |
| **Key columns** | `variety`, `points`, `price`, `country`, `province`, `winery`, `description` |

> 📥 The raw CSV is not included in this repo due to size/licensing. Download it from Kaggle and place it
> in the working directory before running the notebook.

---

## 🧹 Data Cleaning Steps

1. **Dropped the stray `Unnamed: 0` index column** carried over from the CSV export
2. **Checked and removed duplicate rows**
3. **Handled missing values**:
   - Numeric columns → filled with the **column mean**
   - Categorical columns → filled with the **column mode** (falling back to `"Unknown"` if no mode exists)
4. **Validated** that the dataset was duplicate-free and null-free before moving to EDA

```python
# Numeric imputation
def numeric(df):
    numeric_col = df.select_dtypes(include=np.number).columns
    for col in numeric_col:
        if df[col].isna().sum():
            df[col].fillna(df[col].mean(), inplace=True)
    return df

# Categorical imputation
def categorical(df):
    categorical_col = df.select_dtypes(include='object').columns
    for col in categorical_col:
        mode = df[col].mode()
        df[col].fillna(mode[0] if not mode.empty else 'Unknown', inplace=True)
    return df
```

---

## 📊 Exploratory Analysis

The EDA focuses on the relationship between **wine variety**, **points (rating)**, and **price**, narrowed
to the **top 15 most-reviewed varieties** for readability:

| Plot | What it shows |
|---|---|
| **Bar plot** | Average points per top-15 variety |
| **Box plot** | Spread and outliers of points per variety |
| **Violin plot** | Full distribution shape of points per variety |
| **Count plot** | Review volume per variety |
| **Scatter plot** | Points vs. price (log-scaled) across the full dataset |
| **Facet plot** | Points vs. price, split by the top 6 varieties |
| **Histograms** | Distribution of points and of price |
| **Boxen plot** | Price distribution across varieties |

---

## 🛠️ Tech Stack

- **Python** — pandas, numpy
- **Visualization** — matplotlib, seaborn
- **Environment** — developed in Google Colab / Jupyter

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/jaminjuma/<repo-name>.git
cd <repo-name>

# Install dependencies
pip install pandas numpy matplotlib seaborn

# Download winemag-data-130k-v2.csv from Kaggle and place it in the project folder,
# then run the notebook/script
python wine_dataset_cleaning.py
```

---

## 🔮 Possible Next Steps

- Feature engineering from the `description` text column (e.g., sentiment or keyword extraction)
- A regression model predicting `points` or `price` from wine attributes
- Country/region-level breakdowns of quality and pricing trends

---

## 👤 Author

**Jamin Juma**
Founder of [Automateke](https://automateke.app) · CS student, Kirinyaga University

- 🌐 Portfolio: [jaminjuma.tech](https://jaminjuma.tech)
- 💻 GitHub: [@jaminjuma](https://github.com/jaminjuma)
- 🔗 LinkedIn: [jumajamin](https://linkedin.com/in/jumajamin)

---

## 📄 License

This project is licensed under the MIT License — feel free to use and adapt it.
