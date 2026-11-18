# Boston Airbnb Price Analysis

An ST 552 project by Peter Sasu and Vincent Johnson Attakpah that uses multiple linear regression to study what drives the nightly prices of Airbnb listings in Boston.

**Interactive map:** [Boston Neighborhood Price Map](https://vincent-attakpah.github.io/Boston-airbnb-price-analysis/)

## Research questions

1. How do property characteristics (number of guests, bedrooms, bathrooms, shared bathrooms and room type) relate to nightly price, and do their effects diminish for larger properties?
2. After accounting for property characteristics, how much does price differ across Boston neighborhoods?
3. Does the price premium for each additional guest differ between entire homes and private or shared rooms?

## Data

Boston listings from [Inside Airbnb](https://insideairbnb.com/get-the-data/). After removing listings without a price or with missing predictor values, the analysis uses 3,331 listings. The response is log nightly price.

## Main findings

- **Property characteristics:** the price increase per additional guest diminishes for larger listings, from about 10% (1 to 2 guests) to about 1% (8 to 9 guests). Each additional bathroom adds about 26%, a shared bathroom lowers the price by about 42%, and private or shared rooms are about 21% cheaper than entire homes.
- **Location:** neighborhood adds about 7 percentage points to adjusted R² (0.660 to 0.729). Compared with Downtown, comparable listings cost 34% to 47% less in the outer neighborhoods, while Chinatown and South Boston Waterfront are about 18% to 23% more expensive.
- **Interaction:** an extra guest raises the price of a private or shared room by about 16%, against about 9% for an entire home. In dollars, the premium is still larger for entire homes because they start from a higher price.

The final model predicts held-out listings with a test RMSE of 0.389 on the log scale, close to its cross-validated error.

## The map

`index.html` is a self-contained interactive map of the neighborhood results from Model 2. Each listing is a dot colored by its neighborhood's estimated price difference from Downtown. Clicking a neighborhood shows its percentage and dollar difference, 95% confidence interval, p-value and number of listings.
