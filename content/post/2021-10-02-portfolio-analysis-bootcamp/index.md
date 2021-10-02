---
title: 'Portfolio Analysis Bootcamp '
author: R package build
date: '2021-10-02'
slug: portfolio-analysis-bootcamp
categories: []
tags: []
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
## Portfolio Analysis

Diversify investment -> porfolio -> increase return’s expectation and reduce the risk. Hence, we need to test our investment strategy, it is called: back testing. Back testing are tested using historical data. We also need to use an online performance monitoring.

## Import Data
```{r}
library(tidyquant)
ko <- getSymbols("ko", from = "2003-01-01", to = "2016-08-30", auto.assign = FALSE)
pep <- getSymbols("pep", from = "2003-01-01", to = "2016-08-30", auto.assign = FALSE)
head(cbind(ko, pep))
```

## Portfolio Analysis

Diversify investment -> porfolio -> increase return’s expectation and reduce the risk. Hence, we need to test our investment strategy, it is called: backtesting. Backtesting are tested using historical data. We also need to use an online performance monitoring.

## Import Data
```{r}
library(tidyquant)
ko <- getSymbols("ko", from = "2003-01-01", to = "2016-08-30", auto.assign = FALSE)
pep <- getSymbols("pep", from = "2003-01-01", to = "2016-08-30", auto.assign = FALSE)
head(cbind(ko, pep))
```

## Data Manipulation

First, we define ko_pep as the ratio expressing the value of the share price of the Coca Cola company in terms of the share price of PepsiCo.

```{r}
ko <- Ad(ko)
pep <- Ad(pep)
head(cbind(ko, pep))
```

```{r}
ko_pep <- ko/pep
head(ko_pep)
```


## Get a feel for the data

The choice of investment matters even when the underlying risky assets are similar. As a first example, let us consider the stock price of the Coca Cola Company and the PepsiCo company from January 2003 until the end of August 2016.

The time series plot shows you the value evolution of one dollar invested in each company. As an exercise, plot the time series showing the relative value of an investment in the Coca Cola company, compared to the value of an investment in PepsiCo. To do this exercise, you can use the corresponding price series, available as the variables ko and pep in your workspace.

Three important packages that you will use in this module are the xts and zoo packages and the PerformanceAnalytics package.

Instructions
1. Define ko_pep as the ratio expressing the value of the share price of the Coca Cola company in terms of the share price of PepsiCo.
2. Use plot.zoo() to visualize the variation in this ratio over time. Note that when the value of the ratio is larger than 1, the performance of ko since January 2003 is higher than that of pep.
3. As a reference line, use abline() to include a horizontal line at h=0.5. Note that where the value of the ratio is larger than one, the Coca Cola Company outperforms Pepsico and vice versa.

```{r}
# Define ko_pep 
# ko_pep <- 

# Make a time series plot of ko_pep
  plot.zoo(ko_pep)
# Add as a reference, a horizontal line at 0.5
  graphics::abline(h=0.5)
  
```


## Calculating portfolio weights when component values are given

In the video, it was shown that you can easily compute portfolio weights if you have a given amount of money invested in certain assets. If you want to start investing in a portfolio, but you have budget restraints, you can also impose weights yourself. Depending on what these are, you will invest a certain amount of money in each of the assets based on their weight.

When given asset values, calculating the weights is quite simple. Recall from the video that weights are calculated by taking the value of an asset divided by the sum of values from all assets.

In this exercise, you will learn to calculate weights when individual asset values are given! For this example, an investor has 4000 USD invested in equities, 4000 USD invested in bonds, and 2000 USD invested in commodities. Compute the weights as the proportion invested in each of those three assets.
Instructions

1. Define the vector values as the vector holding the three asset values.
2. Define the vectors weights as the vector values divided by the total value (obtained by summing over the component values using the function sum().
3. Print weights.

```{r}
# Define the vector values
values <- c(4000,4000,2000)

# Define the vector weights
weights <- values/sum(values)

# Print the resulting weights
print(weights)
```

## The weights of a market capitalization-weighted portfolio

In a market capitalization-weighted portfolio, the weights are given by the individual assets' market capitalization (or market value), divided by the sum of the market capitalizations of all assets. A typical example is the S&P 500 portfolio invested in the 500 largest companies listed on the US stock exchanges (NYSE, Nasdaq). Note that by dividing by the sum of asset values across all portfolio assets, the portfolio weights sum to unity (one).

As an exercise, inspect the distribution of market capitalization based weights when the portfolio is invested in 10 stocks. For this exercise, you can use market capitalizations of 5, 8, 9, 20, 25, 100, 100, 500, 700, and 2000 million USD.
Instructions


1.  Define the vector marketcaps holding the market capitalizations.
2. Calculate the weights of marketcaps and assign them to weights.
3. Print a summary of weights.
4. Create a bar plot of weights.

```{r}
# Define marketcaps
 mkt.cap <- c(5,8,9,20,25,100,100,500,700,2000)
sum(mkt.cap)

# Compute the weights
weights <- mkt.cap/sum(mkt.cap)

# Inspect summary statistics
summary(weights)

# Create a bar plot of weights
barplot(weights)
  
```

## Calculation of portfolio returns

For your first exercise on calculating portfolio returns, you will verify that a portfolio return can be computed as the weighted average of the portfolio component returns. In other words, this means that a portfolio return is calculated by taking the sum of simple returns multiplied by the portfolio weights. Remember that simple returns are calculated as the final value minus the initial value, divided by the initial value.

Assume that you invested in three assets. Their initial values are 1000 USD, 5000 USD, 2000 USD, respectively. Over time, the values change to 1100 USD, 4500 USD, and 3000 USD.

Instructions

1. Create a vector of the initial asset values in_values.
2. Create a vector of the final values, fin_values.
3. Create a vector of the initial weights, weights.
4. Use the simple return definition to compute the vector of returns on the three component assets. Assign return values to returns.
5. Assign the portfolio returns to preturns.

```{r}
# Vector of initial value of the assets
in_values <- c(1000,5000,2000)
  
# Vector of final values of the assets
fin_values <- c(1100,4500,3000)

# Weights as the proportion of total value invested in each asset
weights <- in_values/sum(in_values)

# Vector of simple returns of the assets 
returns <- (fin_values - in_values)/in_values
  
# Compute portfolio return using the portfolio return formula
preturns <- sum(returns*weights)
  
```

## From simple to gross and multi-period returns

The simple return R expresses the percentage change in the value of an investment. The corresponding so-called "gross" return is defined as the future value of 1 USD invested in the asset for one period and is thus equal to 1 + R.

The gross return over two periods is obtained similarly. Let $R1$ be the return in the first period and $R2$ the return in the second period. Then the end-value of a 1 USD investment is (1 + $R1$)*(1 + $R2$).

The corresponding simple return over those two periods is:
(1 + $R1$)*(1 + $R2$) - 1.

Suppose that you have an investment horizon of two periods. In the first period, you make a 10% return. But in the second period, you take a loss of 5%.

Compute the end value of a 1000 USD investment.

```{r}
(1 + 0.1) * (1 - 0.05)
```




## The asymmetric impact of gains and losses

It is important to be aware of the fact that a positive and negative return of the same relative magnitude do not compensate each other in terms of terminal wealth. Mathematically, this can be seen from the identity $(1 + x) * (1 - x) = 1 - x^2$, which is less than one. A 50% loss is thus not compensated by a 50% gain. After a loss of 50%, what is the return needed to be at par again? Verify your answer in the R console.

```{r}
(1 - 0.5) * (1 + 1)
```



## Buy-and-hold versus (daily) rebalancing

The choice of investment matters, even when the underlying risky assets are similar. As an example, you will now consider the stock price of Apple and Microsoft from January 2006 until the end of August 2016. The time series plot shows you the value evolution of one dollar invested in each of them.

For this exercise, your portfolio approach will be to invest half of your budget in Apple stock, and the other half of your budget in Microsoft stock. Over time, the portfolio weights will change. You will have two choices as an investor. The first choice is to be passive and not trade any further. This is called a buy and hold strategy. The second choice is to buy and trade at the close of each day that results in a rebalance of the portfolio such that your portfolio is equally invested in shares of Microsoft and Apple. This is a rebalanced portfolio. 

Which of the following statements is false?

1. By investing in a portfolio of risky assets, the portfolio payoff will be in between the minimum and maximum of the payoff of the underlying risky assets.
2. By investing in a portfolio of risky assets, the risk of the portfolio payoff will be less than the maximum risk of the underlying risky assets.
3. An investor needs to have a lot of capital to be able to invest in a portfolio of many assets.
4. Because the prices of Microsoft and Apple have evolved differently, the investor who spent initially half of his wealth on Microsoft and Apple ends up with a portfolio that is no longer equally invested.



## The time series of asset returns

Calculating the returns for one period is pretty straightforward to do in R. When the returns need to be calculated for different dates the functions Return.calculate() and Return.portfolio(), in the R package PerformanceAnalytics are extremely helpful. They require the input data to be of the xts-time series class, which is pre-loaded. You will explore the functionality of the PerformanceAnalytics package in this exercise.


1. Load the package PerformanceAnalytics in your R session.
2. Have a look at the first and last six rows of prices, using head() and tail() respectively.
3. Use the function Return.calculate() with the only argument prices to compute for each date the return as the percentage change in the price compared to the previous date, call this returns.
4. Print the first six rows of returns.
5. Remove the first row of returns.

```{r}
# Load package PerformanceAnalytics 
library(PerformanceAnalytics)

# Print the first six rows and last six rows of prices
AAPL <- getSymbols("AAPL", from ="2006-01-01", to="2015-08-31", auto.assign = FALSE)[,6]
MSFT <- getSymbols("MSFT", from ="2006-01-01", to="2015-08-31", auto.assign = FALSE)[,6]
prices <- head(cbind(AAPL,MSFT))

# Create the variable returns using Return.calculate()  
returns <-  Return.calculate(prices)

# Print the first six rows of returns. Note that the first observation is NA because there is no prior price.
head(returns)

# Remove the first row
returns <- returns[-1,]
head(returns)