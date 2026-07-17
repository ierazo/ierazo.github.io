---
layout: page
title: Reinventing Order Picking at Amazon Robotics Fulfillment Centers
description: Algorithms and intelligence for large-scale robotic-assisted order fulfillment.
img:
importance: 0.3
category: work
---

Since joining Amazon Fulfillment Technologies in 2024, my main line of work has been the new generation of large-scale online optimization models that decide, in real time, how picking work is assigned across machines and human associates in Amazon Robotics fulfillment centers. These are tri-partite assignment problems of enormous scale, solved continuously as orders arrive, and the resulting algorithms are deployed in North American and European fulfillment centers [(see video)](https://www.youtube.com/watch?v=NZTVgExZqoI), where they orchestrate [very cool robots](https://www.aboutamazon.com/news/operations/amazon-fulfillment-center-robotics-ai).

Two research threads have grown out of this work. The first uses machine learning to speed up large-scale optimization itself: learned models shrink the feasible region the solver must explore, improving convergence speed without degrading solution quality. The second, *learning to configure optimization models*, infers the best model parameters and configuration for online problems that must be solved in real time, improving resiliency and the main operational KPIs.

I have presented this work at the INFORMS Annual Meetings in Seattle (2024) and Atlanta (2025) under the title *Reinventing Order Picking at Amazon Robotics Fulfillment Centers &ndash; Algorithms and Intelligence*, and at Amazon's Modeling and Optimization Seminar (2025). Two related peer-reviewed papers appeared at internal venues in 2025 (Amazon Consumer Science Summit and the Amazon Robotics Conference); their contents remain Amazon-confidential.
