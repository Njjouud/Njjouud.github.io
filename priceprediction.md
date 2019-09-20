---
layout: page
title: Smartphones' Prices Prediction
---


### Purpose

Predicting features that affect smartphones’ prices the most.

### Methodology

Selenium to scrap data from [Souq](https://saudi.souq.com/sa-en/).

### Dataset
#### Data Points
1280 row.

#### Features
* Brand.
* Color.
* Storage.


### Work Stages
#### Web Scraping

From:[Souq](https://saudi.souq.com/sa-en/).

#### Data Cleaning

* Removing Nan values.
* Removing duplicates.
* Creating dummy varibles for categocial data.

#### Baseline Model

Linear Regression Model with R-squared = 0.790.

#### Feature Engineering

* Calculate log2 of storage.
* Calculate log of price.

#### Building,Validating and Testing Model

After doing some feature engineering R-squared has increased to 0.875.

### Target-Price- Distribution 
Target distribution after doing log transformation to remove the skewness.

![distribution]({{ site.url }}/images/price_log_dist.png)

### Correlation Matrix
#### Heatmap

Hypothesis: Storage seems to has the most impact on price.

![correlation]({{ site.url }}/images/heat_map.png)

### Result
#### Residual Polt

![Residual]({{ site.url }}/images/residual.png)

#### Testing

Predicting smartphones' prices in the test dataset and compare them against actual prices. -prices are logged-

![test]({{ site.url }}/images/predicted_against_actual.png)

### Takeaway

Storage is the most influnctial feature with a positive coeffecient.

### Conclusion

If the company was producing smartphones and wants to increase their prices they should increase phones storage first, But
if it was selling smartphones then it can increase Apple smartphones with higher storage capacity.

Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!

### Appendix
#### Appendix A -Features' Coefficients-

![coefficients]({{ site.url }}/images/coeffecients.png)