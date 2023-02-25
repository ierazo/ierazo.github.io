---
layout: page
title: Simulation of Ride-Hailing Systems
description: Analysis and optimization of drivers' behaviors for the system.
img: assets/img/wsc_rides_project/Mapa1.png
importance: 1
category: work
---

Over this project we created what was meant to be the most-detailed/comprehensive open-source ride-hailing system simulator. We put together a model that allowed us to test and simulate different drivers' behaviors, with the goal of realizing the impact of such behaviors in the ride-hailing system and optimize accordingly. 

Most of our code and some brief documentation is available in <a href="https://github.com/ierazo/Ride-Hailing-systems-simulation"> this GitHub repository</a>. This work is summarized in the following <a href="../../assets/pdf/conference_papers/2021_WSC_RideHailing.pdf"> WSC Paper</a>, which was presented in that conference with these <a href="../../assets/pdf/presentations/presentation_wsc_2021.pdf"> slides</a>. The main contribution of this paper is that **our model is the most detailed in the literature**, and that it can be used **under any conditions of a real-world ride-hailing system**. We used the San Francisco metropolitan area as our case study, and the main results for four drivers' policies are shown in the embedded pdf below:

<embed src="../../assets/img/wsc_rides_project/MapaTriple_opt.pdf" width="1200" height="1200" 
 type="application/pdf">

Our model is extremely detailed, and as such it is the first work showing the disparity of metrics (time waiting, service level, ...) over different districts/areas for the ride-hailing system under different policies; and under different times of the week (pdf above only shows one sneek peak). Going into more detail of this project, basically, this problem is characterized by four main components: 

1. Multiple actors: drivers, riders, ride-hailing company.
2. Heterogenous drivers and riders, each with their own preferences.
3. Decisions being made in real-time, with algorithms and logic developed by ride-hailing companies taking over.
4. Events modifying the state of the system after happening. For example, a "pick-up" event makes the driver busy (cannot take other passengers), makes the customer satisfied, and generates instantly a future event of "drop-off" where the same driver and rider are involved, and the time to that event depends on the events before plus the route selected. 

In order to solve this problem we came up with a very flexible framework, where each driver and rider is an instance of an object, having multiple attributes that define them; and where all of these attributes can then be set up easily using real-world data. We also proposed a methodology with events as objects that would interact within each other, having specific guidelines for those interactions, all over a sorted list of events that allowed us to simulate in real-time the ride-hailing system. More details can be found in the paper, and a brief flowchart of the simulation procedure is presented below:

<embed src="../../assets/img/wsc_rides_project/SimulationFullProcedure.pdf" width="1200" height="1200" 
 type="application/pdf">

In order to perform the case study we had to analyze a lot of spatio-temporal data, and merge many different data sources. This required multiple rounds of data cleaning/preparation and also mappings between different data sources. Some of the main challenges are shown below:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/wsc_rides_project/Mapa1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/wsc_rides_project/Mapa2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, data corresponding to actual taxi/cab drivers' behaviors had granularities at larger levels, and gave information of origin/destination pairs; that being said we had to adjust the data to create corresponding distribution matrices for their movements. On the right, the elevation of San Francisco differs greatly, and we considered those differences to compute the shortest path times (time distances) between drivers and riders such as to perform the ride-hailing assignments. We used real-world data on distances, and average speeds for different streets.  
</div>


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/wsc_rides_project/Mapa3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The spatio-temporal distribution of arrivals into the system is non-homogeneous, and as such we needed to reflect the correct rate of arrivals for each area in the city.
</div>

