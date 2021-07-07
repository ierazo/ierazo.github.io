---
layout: page
title: ML Project
excerpt: "Recent Presentations"
---

###### For the graduate machine learning course (CS7641) from the Computer Science Department in Georgia Tech we are required to perform a project using supervised and unsupervised machine learning algorithms. Having said that, our group decided to develop a Portfolio-Building (stocks) procedure with the goal of exceeding robo-traders' rate of return without the requisite of paid data. A video version of our initial proposal can be found [ [HERE](https://www.youtube.com/watch?v=NICXLeaeBtY) ]; and below the team's member names we present a midterm report on our project. Feel free to reach us if you are interested.

### Team members
- [Dylan Yung](https://www.linkedin.com/in/dylan-yung-4544a6149/)
- [Munindar Meena](https://www.linkedin.com/in/munindarkr/)
- Manuel Fernandez
- Ignacio Erazo

# **Data-Driven Portfolio Creation**
## Introduction/Background
In business circles the word ''investment'' refers to acquired assets or items that generate income or appreciate, generating future wealth. Given the social structure we live in (where money is needed to have access to goods and services), most people seek investments in high-performing assets to meet their future needs. This behavior is evidenced by the fact that more than 52% of the American families have either indirect or direct investments in the stock market [1].

The performance of the stock market is evaluated by indices, which are defined as ''statistically representative samplings of any set of observable securities in a given market segment''. Examples of indices include the S&P 500 (a representation of the large-cap segment of the US equity market) and the MSCI Europe Information Technology Index (a representation of IT companies in large and mid-cap segments across 15 Developed
Markets countries in Europe). Indices are used as a benchmark to measure the performance of an investment portfolio; but they are not financial products, so they cannot be bought or sold.

Optimizing an investment portfolio has always been an attractive problem because of its economical implications. In 1952 it was theorized that the stock market is the ''perfect portfolio'' because it allows the maximum diversification of assets [2]. In 1965 it was documented that is extremely uncommon for active stock traders to outperform the market consistently over time [3]. In 1976 the first index mutual fund (Vanguard 500 Index fund, mimicking the S&P 500 index) was created, with the goal of providing a ''passive'' investment method that requires minimal transaction fees and generates returns that approximate the market's return. Today there exist thousands of Index Mutual Funds and financial products linked to the performance of indices; however, the following question stands: Can we use previous market information in order to create a portfolio that outperforms the market return?

## Literature Review and Problem Definition

There exist several investment-related problems that have been studied over the years, and two of the most prominent are the stock trading problem and the portfolio optimization problem. Solving these problems is very difficult as it is usually required to accurately forecast the future performance of the stocks or their future prices, and that in itself is a difficult problem, evidenced by recent works focused only on forecasting the direction of the price in the future (generative neural networks [4] and deep learning [5]) with less than stellar results. Most of the studies for this sub-problem use historical data to perform a time-series analysis.  


The stock trading problem seeks to maximize returns by selling and buying stocks over short periods of time, basically mimicking the behavior of a ''daily'' stock trader or a ''swing'' trader, and recent techniques used are deep learning [6] and deep reinforcement learning [7].

We focus on the portfolio optimization problem, which seeks to build a portfolio of stocks to be held over a longer period of time; basically mimicking ''buy and hold'' traders. This is also closer to the idea of passive investing. This problem has been studied extensively in the optimization literature, and we refer the reader to [8] for a comprehensive review on the methods used to solve this problem under several variants. Recently, machine learning methods have also been used [9,10] to tackle this problem.


In simple terms, our problem statement is: Given historical data for a set of stocks overtime period [a,b], can we leverage this information to create a portfolio, comprised by a subset of those stocks, whose return matches or exceeds the market rate of return (performance) over some period [b,c]?


## Methods
In our dataset each row corresponds to a datapoint of a given stock and columns are relevant attributes. Our first step will be to clean the data (as example, stocks that do not exist anymore) and eliminate some redundant columns. Afterwards, we will add columns to the data set in the form of technical indicators (i.e., functions of basic stock statistics such as: prices,  shares outstanding, ...) which have been proven to be relevant for trading performance.

In order to create our portfolio our goal is to rank the companies according to some measure of how well they will perform in the future (for example: "probability of being a high performing stock") and use this ranking in a smart way to decide the portfolio composition. So far our plan is:
- Use unsupervised methods to cluster companies. The output may reduce the number of companies to rank. Also, the clusters' label of stocks will be used as input for the supervised methods.
- For supervised learning we are thinking of using a Deep Learning ranking algorithm similar to YouTube's recommendation algorithm [1]. This may allow us to create a ranking of the best candidate stocks for our portfolio. Examining methodologies from indices like the S&P 500 [9], we discovered they have several rules to update its stocks' composition. The ranking method will be helpful, as after new data entries are available we can update the rankings and adjust our portfolio.


## Potential results and Discussion

Robo-traders/advisors have a typical rate of return below 5% [6] and index funds historically have a median annual rate of return of 10%. Exceeding robo-traders' rate of return is our goal, but we expect to be below typical index funds' rates. Our methodology will not rely on private or proprietary data, so we expect our model to generalize under different markets and be replicable; however the lack of "expert" information may not allow us to get an optimal rate of return.

## Bibliography
- [1] Board of Governors of the Federal Reserve System. "Survey of Consumer Finances (SCF)". [link](https://www.federalreserve.gov/econres/scfindex.htm)
- [2] Harry Markowitz. "Portfolio Selection". *The Journal of Finance* 7.1 (1952), pp. 77–91
- [3] Eugene F. Fama. "The Behavior of Stock-Market Prices". *The Journal of Business* 38.1 (1965), pp. 34–105. issn: 00219398, 15375374.
- [4] Jefferson  Hernandez  and  Andres  G.  Abad.  ''Learning  from  multivariate discrete sequential data using a restricted Boltzmann machine model''. *In 2018 IEEE 1st Colombian Conference on Applications in Computational Intelligence  (ColCACI)*. (2018),  pp.  1–6. doi:10.1109/ColCACI.2018.8484854.
- [5] Alexiei Dingli and Karl Fournier. ''Financial Time Series Forecasting – A Deep Learning Approach''. *International Journal of Machine Learning and Computing* 7 (2017), pp. 118–122. doi:10.18178/ijmlc.2017.7.5.632.
- [6] Thomas G. Fischer and C. Krauss. ''Deep learning with long short-term memory networks for financial market predictions''. *European Journal of Operations Research* 270 (2018), pp. 654–669.
- [7] Yue Deng et al. ''Deep Direct Reinforcement Learning for Financial Signal Representation and Trading”. *IEEE Transactions on Neural Networksand  Learning  Systems* 28.3  (2017),  pp.  653–664. doi:10.1109/TNNLS.2016.2522401
- [8] Prisadarng Skolpadungket. "Portfolio management using computational intelligence approaches". PhD thesis. University of Bradford, 2013.
- [9] Steve Y. Yang and Saud Almahdi.  "An adaptive portfolio trading system: A risk-return portfolio optimization using recurrent reinforcement learning with expected maximum drawdown". *Expert Systems with Applications* (2017).
- [10] Steve Y. Yang, Qiang Song and Anqi Liu. "Stock portfolio selection using learning-to-rank algorithms with news sentiment". *Neurocomputing* (2017).
- [666] Paul Covington, Jay Adams, and Emre Sargin. "Deep Neural Networks for YouTube Recommendations". *Proceedings of the 10th ACM Conferenceon Recommender Systems.* New York, NY, USA, 2016
- [6] "Robo-Advisor Performance Is Only One Piece of the Puzzle". [link](https://www.nerdwallet.com/article/investing/robo-advisor-performance).
- [9] SP U.S. Indices Methodology. [link](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)
