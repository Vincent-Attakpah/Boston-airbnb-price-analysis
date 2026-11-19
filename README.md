# Boston Airbnb Price Analysis

An ST 552 project by Peter Sasu and Vincent Johnson Attakpah that uses multiple linear regression to study what drives the nightly prices of Airbnb listings in Boston.

**Interactive map:** [Boston Neighborhood Price Map](https://vincent-attakpah.github.io/Boston-airbnb-price-analysis/)

## Research questions

1. How do property characteristics (number of guests, bedrooms, bathrooms, shared bathrooms and room type) relate to nightly price, and do their effects diminish for larger properties?
2. After accounting for property characteristics, how much does price differ across Boston neighborhoods?
3. Does the price premium for each additional guest differ between entire homes and private rooms?

## Data

Boston listings from [Inside Airbnb](https://insideairbnb.com/get-the-data/). After removing listings without a price or with missing predictor values, and the 4 shared rooms (too few to model as a separate room type), the analysis uses 3,418 listings. The response is log nightly price.

## Main findings

- **Property characteristics:** the price increase per additional guest diminishes for larger listings, from about 10% (1 to 2 guests) to under 2% (8 to 9 guests). Each additional bathroom adds about 25%, a shared bathroom lowers the price by about 42%, and private rooms are about 16% cheaper than entire homes.
- **Location:** neighborhood adds about 7 percentage points to adjusted R² (0.658 to 0.728). Compared with Downtown, comparable listings cost 34% to 46% less in the outer neighborhoods, while Chinatown and South Boston Waterfront are about 18% to 22% more expensive.
- **Interaction:** an extra guest raises the price of a private room by about 15%, against about 10% for an entire home. In dollars, the premium is still larger for entire homes because they start from a higher price.

The final model explains 73% of the variation in log price and predicts held-out listings with a test RMSE of 0.394 on the log scale, close to its cross-validated error.

## The map

`index.html` is a self-contained interactive map of the neighborhood results from Model 2. Each listing is a dot colored by its neighborhood's estimated price difference from Downtown. Clicking a neighborhood shows its percentage and dollar difference, 95% confidence interval, p-value and number of listings.

## Repository contents

| File | Description |
|---|---|
| [`analysis/airbnb_price_analysis.pdf`](analysis/airbnb_price_analysis.pdf) | The full report: data preparation, exploratory analysis, model selection, diagnostics and answers to the research questions |
| [`analysis/airbnb_price_analysis.Rmd`](analysis/airbnb_price_analysis.Rmd) | The R Markdown source for the report |
| [`analysis/listings.csv`](analysis/listings.csv) | Raw Boston listings data from Inside Airbnb |
| [`index.html`](index.html) | The interactive neighborhood price map |

## Methods

- Data cleaning in base R: price parsing, bathroom counts and shared-bathroom indicators extracted from text, distance to downtown from coordinates, and a long-stay indicator for listings requiring 28 or more nights.
- Exploratory analysis: summary statistics, distributions, a correlation heat map and variance inflation factors.
- Model selection on an 80/20 train/test split: backward and forward stepwise selection with AIC and BIC, and the lasso with a cross-validated penalty, compared by 10-fold cross-validation.
- Diagnostics: residual plots, influence measures (leverage and Cook's distance) and a sensitivity analysis without influential listings.
- Inference: three nested models, compared with partial F-tests, with coefficients reported as percentage changes with 95% confidence intervals.

## Reproducing the analysis

Open `analysis/airbnb_price_analysis.Rmd` in RStudio and knit it. It reads `listings.csv` from the same folder and needs the R packages `ggplot2`, `patchwork`, `car` and `glmnet`:

```r
install.packages(c("ggplot2", "patchwork", "car", "glmnet", "rmarkdown"))
```

## Data source and license

The listings data come from [Inside Airbnb](https://insideairbnb.com/), which publishes them under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
