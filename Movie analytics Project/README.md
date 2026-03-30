# 🎬 Movie Industry Correlation Analysis

A data analysis project exploring what factors drive box office revenue in the
movie industry. The dataset covers **7,668 movies released between 1986 and 2016**
and examines relationships between budget, gross revenue, IMDb scores, genres,
content ratings, production companies, and more.

---

## 📌 Project Overview

This project was built to answer key questions about the movie industry:

- Does a bigger budget guarantee more revenue?
- Do higher-rated films earn more at the box office?
- Which production companies dominate gross revenue?
- Which genres are most profitable, and has that changed over the decades?
- Which films delivered the best return on investment regardless of budget size?

---

## 📁 Repository Structure
```
├── Movie_Correlation_Analysis.ipynb   # Main analysis notebook
├── movies.csv                         # Dataset
└── README.md                          # Project documentation
```

---

## 📊 Dataset

| Attribute | Detail |
|---|---|
| Source | Kaggle — Movie Industry Dataset |
| Rows | 7,668 movies |
| Time Period | 1986 – 2016 |
| Columns | 15 |

### Columns

| Column | Description |
|---|---|
| `name` | Movie title |
| `rating` | Content rating (G, PG, PG-13, R, etc.) |
| `genre` | Primary genre |
| `year` | Catalogue year |
| `released` | Theatrical release date |
| `score` | IMDb user rating |
| `votes` | Number of IMDb user votes |
| `director` | Director name |
| `writer` | Writer name |
| `star` | Lead actor/actress |
| `country` | Country of origin |
| `budget` | Production budget (USD) |
| `gross` | Box office gross revenue (USD) |
| `company` | Production company |
| `runtime` | Film duration (minutes) |

---

## 🔧 Project Workflow

### 1. Setup & Data Loading
- Imported `pandas`, `numpy`, `matplotlib`, and `seaborn`
- Loaded dataset using a relative path for portability across machines

### 2. Data Inspection
- Previewed data with `head()`, `info()`, and `describe()`
- Confirmed 7,668 rows across 15 columns

### 3. Data Quality Checks
- Identified and reported missing values per column
- Detected and removed duplicate rows
- Visualised outliers in gross revenue using a box plot
- Replaced `budget = 0` with `NaN` (~28% of rows had zero budgets
  representing missing data, not actual zero-cost productions)

### 4. Feature Engineering
- Extracted `release_year` from the `released` date string using
  `pd.to_datetime()` for robustness
- Created a `decade` column (e.g. `1990s`) for genre trend grouping
- Computed `roi = (gross - budget) / budget` on rows with known budget values

### 5. Exploratory Visualisations
- Budget vs Gross — scatter plot and regression plot
- IMDb Score vs Gross — regression plot
- Content Rating vs Gross — strip plot

### 6. Correlation Analysis
- Pearson correlation on numeric features only
  (`select_dtypes(include='number')`)
- Label-encoded all categorical columns on a separate copy (`df_encoded`)
  to avoid corrupting the original dataframe
- Pearson correlation on all features (encoded)
- Heatmaps with masked upper triangle, `coolwarm` colormap, and annotations
- Identified strongly correlated feature pairs (`|r| > 0.5`)

### 7. Revenue Analysis
- Top 15 production companies by total gross revenue
- Top 15 company-year combinations
- Top 15 movies by ROI — reveals low-budget films often outperform
  blockbusters on a relative basis
- Average gross revenue by genre per decade (1980s–2010s)
- Overall top 5 genres by average gross

---

## 📈 Key Findings

| Finding | Detail |
|---|---|
| Strongest correlator with gross | **Budget** (r ≈ 0.71) |
| Weakest correlator with gross | **IMDb Score** (r ≈ 0.17) |
| Missing budget data | ~28% of rows had `budget = 0`, treated as missing |
| High-ROI films | Tend to be low-budget horror and thriller productions |
| Dataset size | 7,668 rows (original notebook used 6,820) |

---

## 🛠️ Requirements
```
python >= 3.8
pandas
numpy
matplotlib
seaborn
```

Install all dependencies with:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## 🚀 How to Run

1. Clone this repository:
```bash
   git clone https://github.com/your-username/movie-correlation-analysis.git
   cd movie-correlation-analysis
```

2. Install dependencies:
```bash
   pip install pandas numpy matplotlib seaborn
```

3. Launch the notebook:
```bash
   jupyter notebook Movie_Correlation_Analysis.ipynb
```

4. Run all cells from top to bottom (Kernel → Restart & Run All)

> ⚠️ Make sure `movies.csv` is in the **same directory** as the notebook
> before running.

---

## 💡 Potential Future Work

- **Inflation adjustment** — normalise budget and gross values to a single
  base year using CPI data for accurate cross-decade comparisons
- **Spearman correlation** — more robust than Pearson for the skewed
  distributions present in budget and gross columns
- **Predictive modelling** — use budget, genre, runtime, and rating as
  features to predict gross revenue with regression models
- **Sentiment analysis** — incorporate critic review sentiment as an
  additional predictor of box office performance

---

## 👤 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [your-linkedin](https://linkedin.com/in/your-linkedin)

---

## 📄 License

This project is licensed under the MIT License.
