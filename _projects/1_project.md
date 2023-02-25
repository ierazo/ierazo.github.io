---
layout: page
title: Simulation of Ride-Hailing Systems
description: Analysis and optimization of drivers' behaviors for the system.
img: assets/img/wsc_rides_project/Mapa1.png
importance: 1
category: work
---

Over this project we created what was meant to be the most-detailed/comprehensive open-source ride-hailing system simulator. We put together a model that allowed us to test and simulate different drivers' behaviors, with the goal of realizing the impact of such behaviors in the ride-hailing system and optimize accordingly. 

Most of our code and some brief documentation is available in <a href="https://github.com/ierazo/Ride-Hailing-systems-simulation"> this GitHub repository</a>. This work is summarized in the following <a href="../../assets/pdf/conference_papers/2021_WSC_RideHailing.pdf"> WSC Paper</a>, which was presented in that conference with these <a href="../../assets/pdf/presentations/presentation_wsc_2021.pdf"> slides</a>. Basically, this problem is characterized by four main components: 


1. Multiple actors: drivers, riders, ride-hailing company.
2. Heterogenous drivers and riders, each with their own preferences.
3. Decisions being made in real-time, with algorithms and logic developed by ride-hailing companies taking over.
4. Events modifying the state of the system after happening. For example, a "pick-up" event makes the driver busy (cannot take other passengers), makes the customer satisfied, and generates instantly a future event of "drop-off" where the same driver and rider are involved, and the time to that event depends on the events before plus the route selected. 

In order to solve this problem we came up with a very flexible framework, where each driver and rider is an instance of an object, having multiple attributes that define them; and where all of these attributes can then be set up easily using real-world data. We also proposed a methodology with events as objects that would interact within each other, having specific guidelines for those interactions, all over a sorted list of events that allowed us to simulate in real-time the ride-hailing system. Our main contribution is that **our model is the most detailed in the literature**, and that it can be used **under any conditions of a real-world ride-hailing system**. As presented in our paper, we used the San Francisco metropolitan area as our case study, for which we had to perform a lot of data cleaning/mangling/work.



<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>



<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
