---
layout: page
title: ML Project
excerpt: "Recent Presentations"
---

###### For the graduate machine learning course (CS7641) in the Computer Science Department in Georgia Tech we are required to perform a project using supervised and unsupervised machine learning algorithms. Having said that, our group decided to develop a Portfolio-Building (stocks) procedure with the goal of exceeding robo-traders' rate of return without the requisite of paid data. We present a short version of our proposal (500+-50 words) below the team's member names, but reach us if you are interested. A video version of our proposal can be found [here](https://www.youtube.com/watch?v=NICXLeaeBtY)

### Team members
- Dylan Yung
- [Munindar Meena](https://www.linkedin.com/in/munindarkr/)
- Manuel Fernandez
- John Montgomery
- Ignacio Erazo

# **Data-Driven Portfolio Creation**
## Introduction
Investing is a critical component of today's economy, as evidenced by the fact that more than 52% of the American families have either indirect or direct investments in the stock market [3]; therefore optimizing an investment portfolio has always been an attractive problem. The performance of the stock market is evaluated by indices, which are statistically representative samplings of any set of observable securities in a given market segment. In 1952 it was theorized that the stock market is the "perfect portfolio" because it allows the maximum diversification of assets [4]. In 1965 it was documented that is extremely uncommon for active stock traders to outperform the market consistently over time [2].

## (Brief) Literature review
The portfolio optimization problem has been widely studied in the literature, and we refer the reader to [8] for a comprehensive review. Machine learning methods have also been used to tackle this problem [7][5].


## Problem Definition
Given historical data for a set of stocks, can we leverage this information to create a portfolio, comprised by a subset of those stocks, whose return matches or exceeds the market rate of return (performance) in the future?

## Methods
In our dataset each row corresponds to a datapoint of a given stock and columns are relevant attributes. Our first step will be to clean the data (as example, stocks that do not exist anymore) and eliminate some redundant columns. Afterwards, we will add columns to the data set in the form of technical indicators (i.e., functions of basic stock statistics such as: prices,  shares outstanding, ...) which have been proven to be relevant for trading performance.

In order to create our portfolio our goal is to rank the companies according to some measure of how well they will perform in the future (for example: "probability of being a high performing stock") and use this ranking in a smart way to decide the portfolio composition. So far our plan is:
- Use unsupervised methods to cluster companies. The output may reduce the number of companies to rank. Also, the clusters' label of stocks will be used as input for the supervised methods.
- For supervised learning we are thinking of using a Deep Learning ranking algorithm similar to YouTube's recommendation algorithm [1]. This may allow us to create a ranking of the best candidate stocks for our portfolio. Examining methodologies from indices like the S&P 500 [9], we discovered they have several rules to update its stocks' composition. The ranking method will be helpful, as after new data entries are available we can update the rankings and adjust our portfolio.


## Potential results and Discussion

Robo-traders/advisors have a typical rate of return below 5% [6] and index funds historically have a median annual rate of return of 10%. Exceeding robo-traders' rate of return is our goal, but we expect to be below typical index funds' rates. Our methodology will not rely on private or proprietary data, so we expect our model to generalize under different markets and be replicable; however the lack of "expert" information may not allow us to get an optimal rate of return.

## Bibliography
- [1] Paul Covington, Jay Adams, and Emre Sargin. "Deep Neural Networks for YouTube Recommendations". *Proceedings of the 10th ACM Conferenceon Recommender Systems.* New York, NY, USA, 2016
- [2] Eugene F. Fama. "The Behavior of Stock-Market Prices". *The Journal of Business* 38.1 (1965), pp. 34–105. issn: 00219398, 15375374.
- [3] Board of Governors of the Federal Reserve System. "Survey of Consumer Finances (SCF)". [link](https://www.federalreserve.gov/econres/scfindex.htm) 
- [4] Harry Markowitz. "Portfolio Selection". *The Journal of Finance* 7.1 (1952), pp. 77–91
- [5] Steve Y.Yang, Qiang Song and Anqi Liu. "Stock portfolio selection using learning-to-rank algorithms with news sentiment". *Neurocomputing* (2017).
- [6] "Robo-Advisor Performance Is Only One Piece of the Puzzle". [link](https://www.nerdwallet.com/article/investing/robo-advisor-performance).
- [7] Steve Y.Yang and Saud Almahdi.  "An adaptive portfolio trading system: A risk-return portfolio optimization using recurrent reinforcement learning with expected maximum drawdown". *Expert Systems with Applications* (2017).
- [8] Prisadarng Skolpadungket. "Portfolio management using computational intelligence approaches". PhD thesis. University of Bradford, 2013.
- [9] SP U.S. Indices Methodology. [link](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)
