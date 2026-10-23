# Book Market Analytics - Books to Scrape

This folder contains a Jupyter notebook for the Data Science 500 assignment. It scrapes book data from the Books to Scrape demonstration website, cleans the data, explores catalogue patterns, and fits a linear regression model for book prices.

The updated notebook is configured to scrape the first **300 books**. The assignment brief asks for at least 200 books, so the configured sample meets that requirement. The original _500 notebook is retained; use books_to_scrape_live_300.ipynb for the updated version.

> **Data limitation:** Books to Scrape identifies itself as a demo site and says its prices and ratings were randomly assigned. Treat the results as a scraping and modelling exercise, not as evidence about real book markets.

## Files in this folder

- `books_to_scrape_live_300.ipynb` - the updated workflow with a 300-book limit and the seven-column CSV export.
- `sorted books.csv` - the cleaned dataset with only the seven requested output fields.
- `README.md` - this project and run guide.

## Assignment alignment

| Assignment area | What the notebook does |
| --- | --- |
| Data acquisition | Uses Requests and BeautifulSoup to collect 300 product records across listing pages. |
| Required fields | Collects title, GBP price, star rating, stock status, and stock quantity where shown. It also collects genre, description, product URL, and source information. |
| Cleaning and preparation | Standardizes text, converts prices and ratings to numeric fields, derives availability and word counts, removes duplicate products, and drops rows without a title, price, or rating. Missing descriptions are retained as blank. |
| Exploration and visualization | Summarizes prices, ratings, and stock; plots the price distribution, average price by genre, price by rating, and price-rating correlation. |
| Predictive modelling | Fits a linear regression model and compares its held-out results with a training-mean baseline. |
| Professional report | The report is a separate assignment deliverable; this README and notebook do not replace it. |

## Requirements

Use a Python environment with these packages:

- `requests`
- `beautifulsoup4`
- `pandas`
- `numpy`
- `matplotlib`
- `scikit-learn`
- `ipykernel` for running the notebook in VS Code or Jupyter

Install them from a terminal with:

```bash
python -m pip install requests beautifulsoup4 pandas numpy matplotlib scikit-learn ipykernel
```

## Run the notebook

1. Open this folder and open `books_to_scrape_live_300.ipynb` in VS Code or Jupyter.
2. Select the Python environment where the packages above are installed.
3. Make sure the computer has internet access. Before running a live scrape, review the website's current guidance and `robots.txt`.
4. Run the notebook cells from top to bottom. The scraper pauses briefly between requests, so collecting 300 product detail pages can take a few minutes.
5. The cleaning cell writes `sorted books.csv` to the notebook's current working directory. To save it in this folder, set the notebook working directory to this folder before running. The cell prints the full save path when it finishes.

The current scrape limit and delay are set near the top of the notebook:

- `MAX_PRODUCTS = 300`
- `REQUEST_DELAY_SECONDS = 0.25` seconds

## Dataset columns

The generated CSV contains exactly these seven columns, in this order:

| Column | Description |
| --- | --- |
| `Title` | Cleaned book title. |
| `Price` | Numeric price in GBP. |
| `Rating` | Rating label from the site, such as `Five`. |
| `Availability` | Normalized stock status, such as `In Stock`. |
| `Genre` | Category taken from the product page breadcrumbs. |
| `Stock Quantity` | Quantity where shown; out-of-stock entries are set to zero. |
| `Score` | Numeric star rating from 1 to 5, derived from `Rating`. |

The notebook keeps additional fields internally for its analysis and model, but exports only these columns to `sorted books.csv`.
## Model and evaluation

The notebook predicts `price_gbp` using genre, stock status, star rating, and stock quantity. It one-hot encodes the categorical fields, imputes missing numeric predictor values with the median, and uses an 80/20 train-test split with a fixed random seed. It reports MAE, RMSE, and R-squared for both the linear regression model and the training-mean baseline.

Use the metrics and plots produced by your own notebook run when writing the report. Explain the results and limitations in your own words; the sample is the first 300 books in the site's listing order, not a random sample of the full catalogue.

## Assignment report reminder

The assignment also requires a professional project report and the final dataset. Submit the report as a PDF using the specified cover page and signed originality declaration. Follow the brief's formatting requirements: Times New Roman, 12-point font, 1.5 line spacing, and Harvard-style citations and references. For an essay-style report, include a Table of Contents, Introduction, Main Body with relevant subheadings, Conclusion, and References. Discuss methodology, findings, model performance, practical implications, and recommendations.

## Data source

[Books to Scrape](https://books.toscrape.com/) - a demonstration site for practising web scraping. Its displayed prices and ratings are randomly assigned and have no real meaning.
