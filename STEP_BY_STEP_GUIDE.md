# Step-by-Step Guide: Amazon India Sales Analysis

## 0. One-time setup
```bash
git clone https://github.com/<username>/amazon-sales-analysis.git
cd amazon-sales-analysis
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```
Put `amazon.csv` in `data/raw/` (unzip `archive.zip`).

## 1. Two ways to run the project
| Way | Command | Use when |
|---|---|---|
| Notebook (step by step) | `jupyter notebook notebooks/Amazon_Sales_Analysis.ipynb` then Run All | Learning, presenting, screenshots |
| Script (one command) | `python amazon_sales_analysis.py` | Quick re-run, automation |

## 2. What each step does and how you know it is done

| # | Task | Key code | Done when |
|---|---|---|---|
| 1 | Setup | imports, `sns.set_theme` | no import errors |
| 2 | Load | `pd.read_csv("data/raw/amazon.csv")` | shape prints `(1465, 16)` |
| 3 | Inspect | `df.dtypes`, `df.isna().sum()`, `duplicated()` | you see 2 missing rating_count, 1 bad rating (`\|`), 114 duplicate ids |
| 4 | Clean | strip `₹ , %` and convert to numbers, fill median, drop duplicates | rows drop to 1,351 and price columns are numbers |
| 5 | Feature engineering | split `category`, add `discount_amount`, `price_band`, `log_rating_count` | `data/processed/amazon_clean.csv` exists |
| 6 | EDA | 8 plots with Seaborn/Matplotlib | 8 PNG files in `reports/figures/` |
| 7 | Statistical tests | Spearman, Kruskal-Wallis, Mann-Whitney | three p-values printed |
| 8 | Model | Linear Regression and Random Forest, 80/20 split | R2 and MAE table printed |
| 9 | Save | `metrics.json` | file exists in `reports/` |

## 3. Results you should see
- 1,351 unique products, mean rating 4.09, median discount 49%.
- Discount vs rating: Spearman rho = -0.15 (p < 0.001). Heavier discounts go with slightly lower ratings.
- Discount differs across Electronics, Home & Kitchen and Computers & Accessories (Kruskal-Wallis p < 0.001).
- Products above 5,000 INR are rated slightly higher (4.13 vs 4.08, p = 0.014). The gap is small.
- Models: mean baseline MAE 0.213, Linear Regression R2 0.10 / MAE 0.200, Random Forest R2 0.03 / MAE 0.198. Rating is hard to predict from price and discount alone.

## 4. Splitting work between two teammates (so both have commits)
| Member | Branch | Files |
|---|---|---|
| Member 1 | `main` | steps 1-5: data loading, cleaning, features, README |
| Member 2 (Suraj Pamnani) | `feature/analysis` | steps 6-9: plots, tests, model, report |

**Member 1**
```bash
git init
git add data/raw requirements.txt .gitignore README.md
git commit -m "Initial commit: dataset and project setup"
git add notebooks/Amazon_Sales_Analysis.ipynb
git commit -m "Add data loading, cleaning and feature engineering"
git branch -M main
git remote add origin https://github.com/<username>/amazon-sales-analysis.git
git push -u origin main
```
Then add the teammate under Settings > Collaborators.

**Member 2**
```bash
git clone https://github.com/<username>/amazon-sales-analysis.git
cd amazon-sales-analysis
git checkout -b feature/analysis
git add reports/figures
git commit -m "Add EDA visualizations"
git add amazon_sales_analysis.py reports/metrics.json
git commit -m "Add statistical tests and baseline models"
git push -u origin feature/analysis
```
Open a Pull Request on GitHub, have Member 1 review it, then merge. Each person commits from their own GitHub account, so the history shows both.

## 5. Common problems
| Problem | Fix |
|---|---|
| `FileNotFoundError: data/raw/amazon.csv` | Unzip `archive.zip` into `data/raw/` |
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| Plots do not show in a script | They are saved to `reports/figures/`; open the PNG files |
| Notebook cannot find data | Open it from the project folder, or Run All (the first cell moves to the project root) |
