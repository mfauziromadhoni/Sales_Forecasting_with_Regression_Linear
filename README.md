# Retail Store Revenue Prediction — Linear Regression Analysis

A multiple linear regression project built in Excel to model and predict store-level **Revenue** based on location characteristics, marketing investment, and demographic factors. The model was validated on 1,000 historical store records and then used to generate revenue projections for **15 new store locations**.

## Business Problem

A retail chain wants to estimate expected revenue for potential new store locations before committing capital, and to understand which factors most influence store performance. This project builds a regression model that:

- Quantifies the impact of location type, city type, marketing spend, and demographics on revenue
- Identifies which factors are statistically meaningful drivers vs. noise
- Produces a reusable formula to project revenue for candidate store sites

## Dataset

| Detail | Description |
|---|---|
| Observations | 1,000 existing stores (training data) |
| Dependent variable (Y) | Revenue |
| Independent variables (X) | Type of Location (Residential/Commercial), City Type (Metro/Non-Metro), Marketing Sales Investment, Estimated Population in Vicinity, Average Household Income |
| New prediction set | 15 candidate store locations

## Methodology

1. **Preprocessing** — Categorical variables were converted to numeric dummy variables:
   - `Type of Location` → `Location_Residential` (1 = Residential, 0 = Commercial)
   - `City type` → `City_Metro` (1 = Metro, 0 = Non-Metro)
2. **Model fitting** — Built with Excel's **Data Analysis ToolPak → Regression**, using Ordinary Least Squares (OLS) to fit:

   ```
   Revenue = Intercept + β1(Location_Residential) + β2(City_Metro)
             + β3(Marketing Sales Investment) + β4(Estimated Population)
             + β5(Average Household Income)
   ```

   OLS finds the intercept and coefficients that minimize the sum of squared residuals (actual vs. predicted revenue) across all 1,000 observations.
3. **Validation** — Model diagnostics (Significance F, Adjusted R², individual p-values) were reviewed before trusting the coefficients for prediction.
4. **Prediction** — The fitted equation was applied to 15 new store profiles to project expected revenue.

## Model Evaluation Metrics

| Metric | Value | Interpretation |
|---|---|---|
| **Significance F** | 2.80 × 10⁻¹⁷⁴ | Far below the 0.1 threshold — the overall model is highly statistically significant (not due to chance) |
| **Adjusted R²** | 0.5576 | ~55.8% of the variation in Revenue is explained by the model — a solid fit for real-world retail data |
| **R²** | 0.5598 | Consistent with Adjusted R², confirming no major overfitting from the 5 predictors used |
| **Observations** | 1,000 | Training sample size |

## Coefficient Summary

| Variable | Coefficient | P-value | Significant (p < 0.1)? | Interpretation |
|---|---|---|---|---|
| Intercept | 54,941.38 | 3.27 × 10⁻⁸² | — | Baseline revenue when all predictors are 0 |
| Location_Residential | -18,843.36 | 3.01 × 10⁻¹³¹ | ✅ Yes | Residential-area stores earn ~18,843 less revenue than commercial-area stores |
| City_Metro | +4,066.48 | 2.38 × 10⁻¹⁴ | ✅ Yes | Metro-city stores earn ~4,066 more revenue than non-metro stores |
| Marketing Sales Investment | +0.4074 | 7.28 × 10⁻²⁴ | ✅ Yes | Each additional unit of marketing spend adds ~0.407 units of revenue |
| Estimated Population in Vicinity | +0.0316 | 0.7238 | ❌ No | Not statistically significant — excluded from business interpretation |
| Average Household Income | +0.4461 | 1.63 × 10⁻⁴² | ✅ Yes | Each unit increase in household income adds ~0.446 units of revenue |

**Key takeaway:** Location type is the single strongest driver of revenue (largest coefficient magnitude), followed by household income and marketing investment. Estimated population in the vicinity showed no reliable relationship with revenue and was disregarded when interpreting business impact.

## Sample Predictions (15 New Stores)

Applying the fitted equation to 15 candidate store profiles produced the following projected revenue:

| Store # | Location Type | City Type | Marketing Investment | Population (Vicinity) | Household Income | **Predicted Revenue** |
|---|---|---|---|---|---|---|
| 1 | Commercial | Non-Metro | 60,298 | 13,134 | 11,400 | **84,592.67** |
| 2 | Residential | Metro | 49,944 | 16,716 | 10,800 | **65,329.83** |
| 3 | Residential | Metro | 53,124 | 10,348 | 16,800 | **69,301.87** |
| 4 | Residential | Metro | 51,141 | 16,119 | 19,800 | **69,832.22** |
| 5 | Residential | Metro | 57,879 | 14,726 | 19,200 | **72,309.69** |
| 6 | Residential | Non-Metro | 54,340 | 14,527 | 18,600 | **66,533.75** |
| 7 | Residential | Non-Metro | 67,610 | 8,358 | 27,600 | **75,954.79** |
| 8 | Residential | Non-Metro | 55,637 | 11,144 | 22,200 | **68,668.05** |
| 9 | Residential | Metro | 53,396 | 7,960 | 22,200 | **71,821.52** |
| 10 | Residential | Non-Metro | 53,133 | 9,353 | 36,000 | **73,803.80** |
| 11 | Residential | Metro | 49,497 | 9,950 | 15,000 | **67,021.25** |
| 12 | Commercial | Non-Metro | 50,197 | 13,134 | 37,200 | **91,986.29** |
| 13 | Residential | Metro | 63,234 | 14,527 | 13,800 | **72,082.54** |
| 14 | Residential | Non-Metro | 60,059 | 14,129 | 33,600 | **75,554.92** |
| 15 | Commercial | Metro | 66,487 | 9,950 | 16,200 | **93,321.79** |

**Observation:** The three highest-projected stores (#1, #12, #15) are all **Commercial** locations, consistent with the model's finding that commercial locations significantly outperform residential ones. Store #15 (Commercial + Metro + high marketing spend) has the highest projected revenue of the batch.

## Tools Used

- **Microsoft Excel** — Data Analysis ToolPak (Regression add-in)
- Ordinary Least Squares (OLS) regression
- Dummy variable encoding for categorical predictors

## How to Reproduce

1. Enable the Analysis ToolPak: `File → Options → Add-ins → Manage Excel Add-ins → Analysis ToolPak`
2. Encode categorical variables (`Type of Location`, `City type`) into binary dummy columns
3. Go to `Data → Data Analysis → Regression`
4. Set **Input Y Range** to the Revenue column and **Input X Range** to the 5 predictor columns (include headers, check "Labels")
5. Review Significance F → Adjusted R² → individual p-values → coefficients, in that order
6. Apply the resulting equation to new data to generate predictions

## Files

| File | Description |
|---|---|
| `Data` (sheet) | Raw historical data (1,000 stores) |
| `Pre-process` (sheet) | Data with categorical variables encoded as dummies |
| `Regression` (sheet) | Full regression summary output (ANOVA, coefficients, p-values) |
| `Sample` / `Sample Results` (sheet) | 15 new store profiles and their predicted revenue |

## Limitations

- Adjusted R² of ~0.56 means ~44% of revenue variation is driven by factors not captured in this model (e.g., store size, competitor proximity, local management quality)
- Model assumes a **linear** relationship between predictors and revenue; non-linear effects (e.g., diminishing returns on marketing spend) are not captured
- `Estimated Population in Vicinity` was not statistically significant in this dataset and should not be used for business decisions without further investigation
- Predictions assume the new store profiles fall within the same range of values seen in the training data (extrapolation beyond that range is less reliable)
