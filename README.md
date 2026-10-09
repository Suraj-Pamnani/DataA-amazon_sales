# Amazon India Sales Analysis
Exploratory analysis of 1,351 Amazon India products: pricing, discounts, ratings and engagement.

**Team:** Suraj Pamnani and teammate

## Quick start
```bash
pip install -r requirements.txt
python amazon_sales_analysis.py          # full pipeline
jupyter notebook notebooks/Amazon_Sales_Analysis.ipynb   # step by step
```
See `STEP_BY_STEP_GUIDE.md` for the full process, expected results and the two-person Git workflow.

## Structure
```
data/raw/amazon.csv           original data
data/processed/               cleaned data (generated)
notebooks/                    executed project notebook
amazon_sales_analysis.py      one-command pipeline
reports/figures/              9 charts
reports/metrics.json          model results
```
