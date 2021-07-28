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


## Data Collection

Our *base* dataset was a CSV file obtained from the Center for Research in Security Prices (CRSP) with over 25 million rows, and 62 columns, with entries ranging from January 2007 to April 2021. 14940 different securities from different markets were a part of the dataset, rows were **daily** datapoints, and some columns were filled with recurrent information that is usually available everyday (such as opening price, high/low price, shares outstanding, volume traded, among others), whereas other columns indicated extraordinary events or conditions (merging, delisting dates, dividends, among others). In order to meet our desired goal, we had to go over a huge amount of data pre-processing and data cleaning steps, documented as follows:

1. After some preliminary data visualization, it was easy to see that most of the stocks did not have entries over the whole 2007-2021 period (slightly less than 2000 did) which is due to several conditions like bankruptcy, delisting on exchange, merges, among others. From our goal it was clear that we needed to have a subset of stocks with entries over some period and also future information of those stocks to evaluate the performance of our portfolio in the future. Considering that, one naive way to work with our dataset would have been to use the complete time interval (2007-2021) with the stocks will all entries in it; and divide that smaller dataset intro training and testing; however we it would be uninteresting considering that only a few of the stocks would be a part of the dataset, which may bias the analysis (as only big, probably successful companies would have been studied). In the investment-related literature it is usual to divide the training and testing sets into non-overlapping time periods, where the training occurs before the testing, as done by [5] (2003-2013 training set, 2014-2016 testing set) or [6] (23 non-overlapping periods of 1000 days, where the first 750 are testing and remaining 250 are used in trading). Inspired by [6], it was needed to come up with an intelligent way to divide the dataset into smaller datasets (each having a training and testing set) such as to maximize the number of stocks with entries over the whole respective smaller datasets, all while having enough information in each of them (because there is an inverse relationship between the length of time interval covered by a dataset and stocks having entries over the whole time period). 
    After analysing the stucture of the smaller datasets for different values of parameter *k* (where *k* denotes the number of smaller datasets created out of the *base* dataset), we concluded that *k=3* gave the best trade-off between our competing requirements; and so we divided our *base* dataset into one with entries over the 01/2007-12/2011 period, the next over 01/2012-12/2016 period, and the last covering the 01/2017-04/2021 period. This construction was convenient, as it allowed a fairly consistent distribution of the training and testing sets over the time horizon. **For the first two smaller datasets, 4 years would be used as training and to construct the basis of the time-series, and the final year would be the testing set; whereas 3 years 8 months and 8 months would be the duration of the training and testing set (respectively) for the 01/2017-04/2021 dataset.**
    
2. After restricting each of the 3 smaller datasets (denoted as A, B, C from now on, in chronological order) to only the stocks that had entries over the complete respective time period (which was computed by looking at the earliest and latest entry); we realized some of the stocks had entries over the complete periods, but they were too sparse in time. In fact, there was a huge variability in the number of entries for different stocks over the same time period (because of diverse phenomena as: less trading days in some countries, merging, closing/opening the opportunity to buy shares of a stock, maybe even lack of reporting from some of those stocks). In order to have consistent datasets with enough information for each stock, in datasets A, B and C we decided only to consider stocks with: at least 80% of the maximum amount of entries recorded in that respective period (for a single stock), at least one weekly entry, and active status of trading during the whole time period. After applying these rules, 4570, 4759, and 5414 were the respective number of stocks in each of the three smaller datasets.

3. Because we are concerned with building a portfolio with similar behavior as index funds, we decided that our algorithm should predict the rate of return of stocks in the next 4 months, and that way during our testing sets we would be able to adjust our portfolio three times per year (start of the testing set we compute a portfolio, 4 months later we do again, and a third time at the start of month 8). Furthermore, we decided to work with weekly instead of daily data points as that may reduce the noise inherent in daily stock fluctuations; and adjust for the remaining variability in number of entries between different stocks in a same time period. For each stock in each of the three datasets we computed the values of the columns for each week (averaging the numeric values, taking the last value of the week for non-numeric values such as ''NAICS'' code).

4. Afterwards, we started to clean up our three datasets. We read the data description guide of the CRSP and eliminated all redundant (categorization codes from different agencies that basically gave the same information, company name, trading status (as all active), high/low prices (as we don't trade during the day and already have opening price), among others) and useless columns (such as date (not needed as predictive value), market return (we will compare to indices), delisting dates (we care about active stocks), among others). We finally got a total of 12 columns; all of them with no missing values and no stocks with missing rows (weeks).

5. After step 4 we had basic weekly data for all stocks meeting the conditions in the A, B and C time periods; and these datasets were our *basic* datasets. In order to perform feature-engineering and to build-up the time-series, we performed a rigorous analysis on usual technical indicators used in financial time-series. We selected the indicators most suited for long term investment (and widely used) and adjusted them to our weekly data. To each of the *basic* datasets we added the following columns: price moving averages (4, 8, 12, 16 weeks), exponential moving averages (4, 8, 12, 16 weeks); but also their standardized versions as well (dividing by the price of the stock). Moreover, we added Bollinger Band Upper and Lower (BOLU, BOLD respectively) and the standardized versions. Furthermore, we added a standardized weekly volume traded column (dividing by the number of shares available for trading), the Williams-Index-Nice Regime (WINR) and Relative-Strength-Index-Nice-Regime (RSINR). Finally, our ''label'' column was selected to be the 4-month rate of return (in the future); so our dataset uses a time-series containing information up to 4 months earlier, and gives the rate of return over the next 4 months; which is very well suited for our goal of updating the portfolio every four months with the newly received data (as we seek to simulate an index-fund adjustment behavior which helps to avoid huge fees due to constant trading). Now each of the three datasets has around 1.2 million rows and 38 columns plus the label.

## Methods

For this midterm report we have focused on the subproblem of predicting stock prices for companies 4 months into the future. For our first model we parsed each company's data into 4 months chunk in order to a typical index fund re-evaluation period (as example, S&P 500); then our input to the model became 4 months worth of weekly data. We conducted our first few experiments purely with technical indicators and numerical features. We excluded a few categorical features that were of no use because their values were always the same (these columns were useful during the data cleaning process to make sure the companies were trading and some other conditions). Our model is also company agnostic (just looks at raw stock data) in order to build a black boxed model for predicting the rate of return in 4 months (which also gives the future stock price). All results and tests so far are for the stock data from the 01/2017-04/2021 period. 

#### Model Architecture

The input into our model is a 3D tensor of dimension **batch size x 16 weeks x 32 features**, where batch size represents a subset of all the training data, which is 4 month periods of weekly stock data for 5400 companies. This was fed into a 1 dimensional Convolutional Neural Network (CNN), which had a stride of 1, padding of 0, dilation of 1, kernel size of 1. These parameters meant the 1D CNN slides across the rows of each batch in order to learn kernel weights during training. The output for a 1D CNN can be calculated as: **((Number of features + 2 x Padding - Dilation x (Kernel size -1)) / Stride)+1** which is a 1D array of size 32 in our case.

This result was then put through a standard linear neural network layer with an input size of 32 and output size of 16; and finally the result of this process was put through another linear layer of output size 1. This architecture was implemented in order to create a bottleneck and reduce the dimension of features to 1 as our target value is just the rate of return (and stock value) in 4 months after the input. We started with this simple method so we could evaluate its flaws and do do further modifications to avoid them in the future when implementing more methods. Also we thought we could decide on what was the best unsupervised to use depending on our results and the flaws encountered after this first method. 




## Results and Discussion

We show our results in the two figures below, where the first plot shows the result for the training set, whereas the second image shows it for the test set. Each ''epoch" represents 1 run through all the training data, and the objective function is shown for the training and test set. We consider as loss Mean Squared Error (MSE) and it is easy to see that it begins to plateau around 100 epochs. 

![image](/images/MLProject/FigTrain1.png)

![image](/images/MLProject/FigTest1.png)

<!---
<p align="center">
  <img alt="Training set" src="https://github.com/ierazo/ierazo.github.io/blob/main/images/MLProject/FigTrain1.png" width="45%">
  <img alt="Test set" src="https://github.com/ierazo/ierazo.github.io/blob/main/images/MLProject/FigTest1.png" width="45%">
</p>
-->

By looking at the y-axis, we note that the loss over evaluation set is very large, as the scale is over billions; and remains high even for the last epoch (which corresponds to the loss of the test set after training on 500 epochs in the training set). We evaluated our method against a simple linear regression using SKlearn, by flattening the **16 x 32** matrix into just a 384 vector and feeding that as a feature into a linear regression model. SKlearn's linear regression model had an MSE of 1384, which is a lot lower than our model has performed. This could potentially mean that our kernel needs to be larger as the kernel only looks at 1 row in the **16 x 32** matrix and the linear regression model looks at all the rows at once. Learning a weighted kernel of size 1 may be too small to encapsulate all the complexities of stock trends. In future works we will explore compressing the **16 x 32** matrix using unsupervised auto-encoder methods and then feeding that compression through a linear layer to see if we get improved results.

Furthermore, it seems we are just experiencing the difficulty of getting accurate results on the forecast of prices for future stocks, which is a well-known phenomenon in the literature. As our goal is to create a portfolio, our next step is to use our predictions and to build an optimization model on top of it; such as to optimize the resulting portfolio. We still have as goal beating the typical rate of return of Robo-traders/advisors (usually below 5% [11]); and hopefully be close to the performance of the market.

<!--- Preliminary IP formulation
-->
<img src="https://bit.ly/3zLIEwe" align="center" border="0" alt="%\begin{align*}max &\sum_{i \in S}ROR_i y_i + \sum_{i \in S}ROR_i (Q-X_i) \\s.t. & 0<=y_i<=1%\end{align*}" width="317" height="44" />

<!---
## Potential results and Discussion

Robo-traders/advisors have a typical rate of return below 5% [6] and index funds historically have a median annual rate of return of 10%. Exceeding robo-traders' rate of return is our goal, but we expect to be below typical index funds' rates. Our methodology will not rely on private or proprietary data, so we expect our model to generalize under different markets and be replicable; however the lack of "expert" information may not allow us to get an optimal rate of return.
-->

## Bibliography
- [1] Board of Governors of the Federal Reserve System. "Survey of Consumer Finances (SCF)". [link](https://www.federalreserve.gov/econres/scfindex.htm)
- [2] Harry Markowitz. "Portfolio Selection". *The Journal of Finance* 7.1 (1952), pp. 77–91
- [3] Eugene F. Fama. "The Behavior of Stock-Market Prices". *The Journal of Business* 38.1 (1965), pp. 34–105. issn: 00219398, 15375374.
- [4] Jefferson  Hernandez  and  Andres  G.  Abad.  ''Learning  from  multivariate discrete sequential data using a restricted Boltzmann machine model''. *In 2018 IEEE 1st Colombian Conference on Applications in Computational Intelligence  (ColCACI)*. (2018),  pp.  1–6. doi:10.1109/ColCACI.2018.8484854.
- [5] Alexiei Dingli and Karl Fournier. ''Financial Time Series Forecasting – A Deep Learning Approach''. *International Journal of Machine Learning and Computing* 7 (2017), pp. 118–122. doi:10.18178/ijmlc.2017.7.5.632.
- [6] Thomas G. Fischer and C. Krauss. ''Deep learning with long short-term memory networks for financial market predictions''. *European Journal of Operations Research* 270 (2018), pp. 654–669.
- [7] Yue Deng et al. ''Deep Direct Reinforcement Learning for Financial Signal Representation and Trading”. *IEEE Transactions on Neural Networks and  Learning  Systems* 28.3  (2017),  pp.  653–664. doi:10.1109/TNNLS.2016.2522401
- [8] Prisadarng Skolpadungket. "Portfolio management using computational intelligence approaches". PhD thesis. University of Bradford, 2013.
- [9] Steve Y. Yang and Saud Almahdi.  "An adaptive portfolio trading system: A risk-return portfolio optimization using recurrent reinforcement learning with expected maximum drawdown". *Expert Systems with Applications* (2017).
- [10] Steve Y. Yang, Qiang Song and Anqi Liu. "Stock portfolio selection using learning-to-rank algorithms with news sentiment". *Neurocomputing* (2017).
- [11] "Robo-Advisor Performance Is Only One Piece of the Puzzle". [link](https://www.nerdwallet.com/article/investing/robo-advisor-performance).

<!---
- [666] Paul Covington, Jay Adams, and Emre Sargin. "Deep Neural Networks for YouTube Recommendations". *Proceedings of the 10th ACM Conferenceon Recommender Systems.* New York, NY, USA, 2016
- [6] "Robo-Advisor Performance Is Only One Piece of the Puzzle". [link](https://www.nerdwallet.com/article/investing/robo-advisor-performance).
- [9] SP U.S. Indices Methodology. [link](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)
-->
