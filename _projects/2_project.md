---
layout: page
title: Dynamic Portfolio Optimization
description: Creating a trading bot that uses data to adjust a stock portfolio that maximizes value over time.
img: assets/img/trading_project/stocks_up.png
importance: 0.5
category: work
---

This project is under development, and for proprietary reasons details are not explained. We (me and <a href="https://www.linkedin.com/in/dylan-yung-4544a6149/">Dylan Yung</a>) are focused on building a data-driven trading bot that uses Technical Analysis, Machine Learning and Optimization to construct and adjust a stock portfolio over time, with the goal of maximizing the value of such portfolio. This project has required:

1. Several rounds of data preparation, data engineering and time-series analysis.
2. Development and implementation of state-of-the-art ML algorithms.
3. Creating a portfolio-rebalancing optimization algorithm for our application.

So far we have achieved great results, consistently beating most common stock market benchmarks in overall rates of return, so we are trying to expand our work and build an operational trading platform that allows us to deploy our algorithms! :rocket:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/trading_project/rates_return_old.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This figure shows unsupervised clusters of stocks obtained using only our technical analysis. We plot the average rates of returns over different clusters. We can identify over-performing stocks!
</div>
