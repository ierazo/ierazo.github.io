---
layout: page
title: ML Project
excerpt: "Recent Presentations"
---

###### For the graduate machine learning course (CS7641) in the Computer Science Department in Georgia Tech we are required to perform a project using supervised and unsupervised machine learning algorithms. Having said that, our group decided to develop a Portfolio-Building (stocks) procedure with the goal of exceeding robo-traders' rate of return without the requisite of paid data. We present a short version of our proposal (500+-50 words) below the names of the team members, but reach us if you are interested.

### Team members
- Dylan Yung
- Munindar Meena
- Manuel Fernandez
- John Montgomery
- Ignacio Erazo

# **Data-Driven Portfolio Creation**
## Introduction
Investing is a critical component of today's economy, as evidenced by the fact that more than 52% of the American families have either indirect or direct investments in the stock market \cite{StocksFamiles}; therefore optimizing an investment portfolio has always been an attractive problem. The performance of the stock market is evaluated by indices, which are statistically representative samplings of any set of observable securities in a given market segment. In 1952 it was theorized that the stock market is the "perfect portfolio" because it allows the maximum diversification of assets \cite{Markowitz1952}. In 1965 it was documented that is extremely uncommon for active stock traders to outperform the market consistently over time \cite{Fama1965}.

## (Brief) Literature review
The portfolio optimization problem has been widely studied in the literature, and we refer the reader to \cite{ThesisPortfolio} for a comprehensive review. Machine learning methods have also been used to tackle this problem \cite{Almahdi, Song}.


## Problem Definition
Given historical data for a set of stocks, can we leverage this information to create a portfolio, comprised by a subset of those stocks, whose return matches or exceeds the market rate of return (performance) in the future?

## Methods
In our dataset each row corresponds to a datapoint of a given stock and columns are relevant attributes. Our first step will be to clean the data (as example, stocks that do not exist anymore) and eliminate some redundant columns. Afterwards, we will add columns to the data set in the form of technical indicators (i.e. functions of basic stock statistics such as: prices,  shares outstanding, \ldots) which have been proven to be relevant for trading performance.

In order to create our portfolio our goal is to rank the companies according to some measure of how well they will perform in the future (for example: "probability of being a high performing stock") and use this ranking in a smart way to decide the portfolio composition. So far our plan is:
- Use unsupervised methods to cluster companies. The output may reduce the number of companies to rank. Also, the clusters' label of stocks will be used as input for the supervised methods.
- For supervised learning we are thinking of using a Deep Learning ranking algorithm similar to YouTube's recommendation algorithm \cite{45530}. This may allow us to create a ranking of the best candidate stocks for our portfolio. Examining methodologies from indices like the S\&P 500 \cite{SnP}, we discovered they have several rules to update its stocks' composition. The ranking method will be helpful, as after new data entries are available we can update the rankings and adjust our portfolio.


## Potential results and Discussion

Robo-traders/advisors have a typical rate of return below 5% \cite{Robotraders} and index funds historically have a median annual rate of return of 10%. Exceeding robo-traders' rate of return is our goal, but we expect to be below typical index funds' rates. Our methodology will not rely on private or proprietary data, so we expect our model to generalize under different markets and be replicable; however the lack of "expert" information may not allow us to get an optimal rate of return.
