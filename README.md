Amazon India Sales Analysis
A line-by-line guide to the code, the statistics and the reasoning
Suraj Pamnani
October 2026



About Dataset:

o	This project analyses Amazon product data to uncover insights about pricing, ratings, and customer behavior.

o	This dataset is having the data of 1K+ Amazon Product's Ratings and Reviews as per their details listed on the official website of Amazon.

Task:
•	Data Cleaning
•	Exploratory Data Analysis (EDA)
•	Price vs Rating Analysis
•	Category Insights
•	Dataset usecase

What python Libraries or tools gone use:
Tool	Purpose
Python 3.10+	Core language
pandas	Loading, cleaning, grouping and feature engineering
NumPy	Numerical operations, log transforms, binning
Matplotlib	Base plotting and figure export
Jupyter Notebook	Interactive exploration and documentation
Git and GitHub	Version control, branching, pull requests and team collaboration


 1.1	Pipeline:


Steps	Task	Input	Output
1	Setup	Libraries	Ready environment
2	Load	data/raw/amazon.csv	DataFrame, 1,465 x 16
3	Inspect	Raw DataFrame	List of problems found
4	Clean	Raw DataFrame	Numeric columns, 1,351 unique products
5	Feature engineering	Cleaned data	5 new columns, amazon_clean.csv
6	Exploratory analysis	Cleaned data	8 charts
7	Statistical tests	Cleaned data	3 test results with p-values
8	Modeling	Cleaned data	2 models, metrics, feature importance
9	Save	All results	metrics.json, figures, clean CSV



1.2 What we do :
•	analyse 1,351 products on Amazon India, converting textual data into numerical form. 
•	describing the distribution of prices, discounts, and ratings.
•	investigate if these patterns are statistically significant, and finally determine if a machine learning algorithm can predict a product's rating based on its price, discount, and category. 


2. Understanding the Dataset First:
one row is one product listing on Amazon India, scraped in January 2023.
Columns: product_id, product_name, category, discounted_price, actual_price, discount_percentage, rating, etc.

3.process:

I.	imports all the library.

II.	setup block: 

•	sns.set_theme(...) sets one consistent look for every chart (white background with light grid lines, colourblind-friendly palette). Set once, applies everywhere.
•	pd.set_option("display.max_columns", 30) stops pandas hiding middle columns with ... when you print the table.
•	The os.chdir lines fix a common problem. Jupyter runs a notebook from its own folder (notebooks/), so the relative path data/raw/amazon.csv would fail. If the file is not found, the code moves one folder up to the project root.
•	mkdir(parents=True, exist_ok=True) creates reports/figures/ if missing and does nothing if it already exists, so re-running never crashes.



III.	Load and Inspect:

IV.	Cleaning the Data:
•	The conversion function
•	Applying it
•	Removing duplicates
•	A sanity check on the cleaned numbers.

V.	Feature Engineering: 
creating new columns that express information more usefully than the raw columns do.
•	Category hierarchy
•	discount_amount
•	log_rating_count
•	price_band
•	Saving the cleaned dataset

VI.	Exploratory Data Analysis:
Plot helper and subsets
Plot1:Rating distribution
Plot 2: Discount distribution
Plot 3: Products per category (count plot)





Analysis of data set:

Product ID	Name of the Product	Category	Discounted Price	Actual Price	Percentage of Discount	Description about the Product
1351
unique value	1337
unique values	Computer:       16%
Electronics:       5%
Other(1156):  79%	₹199   4%
₹299    3%
Other 93%
	₹999    8%
₹499    5%
Other 87%
	50%     4%
60%     4%
Other 92%
	1293
unique values




1. check for to check Valid, Mismatched, Missing, duplicate.

for product id:
Check	Result
Missing	rating_count is blank in 2 rows. No other column has blanks.
Invalid format	1 row has a non-numeric rating, the "|" entry. Everything else is valid: ids, prices, discount %, rating range, category paths and links.
Mismatched	0 rows. Discount % always matches the prices, discounted price is never above actual price, and each id matches its link. The number of user ids always equals the number of review ids.
Duplicate product_id	206 rows share an id, covering 92 distinct ids. No two rows are fully identical, so the repeats differ in some columns. 1,351 ids are unique.


For other:

Column	Valid	Missing	Mismatched	Duplicates
Product name	1,465	0	0. The same product_id never has two different names.	226 rows share a name with another row, leaving 1,337 distinct names. This is mostly repeated product_id rows. Some are different ids that share one listing title, such as colour variants.
Category	1,465	0	0. The same product_id never has two categories.	Not applicable, since many products share a category. There are 211 distinct category paths under 9 main categories.
Discounted price	1,465	0	Never above actual price. In 3 repeated product_ids the copies show different discounted prices.	Repeated values are normal. There are only 550 distinct prices.
Actual price	1,465	0	Never below discounted price. In 1 repeated product_id the copies show different actual prices.	Repeated values are normal. There are 449 distinct prices.
Discount %	1,465	0	Matches (actual − discounted) / actual within 1 point in every row. Two rows differ only by rounding. In 4 repeated product_ids the copies show different discounts.	Repeated values are normal. There are 92 distinct values.

Product analysis:
Price band	Products	Avg discount %	Avg rating
<500	185	38.65	4.07
500-1K	286	53.27	4.09
1K-5K	575	47.94	4.08
5K-20K	211	46.30	4.09
>20K	94	35.65	4.23

Github link: 
