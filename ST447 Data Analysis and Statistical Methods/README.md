# Comparison of Driving Test Results for a Given Profile between Two Centres

## Overview  

This project compares driving test outcomes at two test centres, Burgess Hill and Wood Green, for a specific candidate profile. The candidate, XYZ, is a 21-year-old woman who lives in Burgess Hill and studies near Wood Green. The analysis helps her choose the centre that offers the best chance of passing.  

## Project goals  

- Compare pass rates between Burgess Hill and Wood Green from 2008–09 to 2023–24.  
- Focus on results for 21-year-old women.  
- Use graphical analysis, normality checks, t-tests and logistic regression to provide a clear recommendation.  

## Data  

- Source: driving test statistics for Burgess Hill and Wood Green between 2008–09 and 2023–24.  
- Variables include age, gender, number of tests conducted and passed and overall pass rates.  
- Summary statistics show similar age distributions across sites, but pass rates consistently favour Burgess Hill.  

The plots on page 3 of the accompanying report show:  

- A line chart of female pass rates by age, where Burgess Hill stays above Wood Green at each age.  
- A time series of pass rates since 2008–09, again with Burgess Hill generally higher, though with more variability.  
- A boxplot for 21-year-old women, which highlights higher median pass rates at Burgess Hill.  

## Methods  

The analysis uses the following steps.  

- Exploratory summary statistics and visualisations for pass rates by centre, age and gender.  
- Normality checks with Q–Q plots and the Shapiro–Wilk test.  
- A Welch two-sample t-test to compare mean pass rates for 21-year-old women at the two centres.  
- Logistic regression modelling to estimate pass probabilities as a function of age, gender and centre.  

The Shapiro–Wilk tests support the use of t-tests, as there is no strong evidence against normality for either centre.  

## How to use this repository  

Typical workflow.  

1. Open the analysis script or R Markdown file.  
2. Load the Excel dataset that contains the yearly statistics for both centres.  
3. Run the data cleaning and transformation steps that convert variables to numeric and factor types.  
4. Recreate the summary tables and plots for overall pass rates, female pass rates and 21-year-old female pass rates.  
5. Run the normality tests and t-tests, followed by the logistic regression model.  

Adjust the file paths and script names to match your setup.  

## Results  

Key findings for 21-year-old women.  

- Average pass rate at Burgess Hill: 45.16 per cent.  
- Average pass rate at Wood Green: 38.83 per cent.  
- The Welch two-sample t-test gives a t-value of about 3.85 and a p-value below 0.001, with a 95 per cent confidence interval for the mean difference from roughly 2.95 to 9.72 percentage points.  
- The results indicate that Burgess Hill has a statistically and practically higher pass rate for this profile.  

Based on these results, the recommendation is that XYZ is more likely to pass at Burgess Hill than at Wood Green.  

## Reproducibility  

To reproduce the analysis.  

- Use the same date range, 2008–09 to 2023–24, and focus on the same age and gender.  
- Apply identical transformations and filters before computing pass rates.  
- Keep the same settings in the t-test and logistic regression models.  

## Acknowledgements and references  

This work was produced as part of the ST447 final project at the London School of Economics and Political Science and relies on official driving test statistics and standard R packages for analysis and visualisation.  
