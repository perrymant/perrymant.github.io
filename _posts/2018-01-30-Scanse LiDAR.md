---
layout: post
title: Scanse LiDAR
excerpt_separator: <!--more-->
---

So I spent today helping out with plotting the output of the Scanse LiDAR sensor.<!--more-->

![Sensor](images/Lidar.jpg)

This LiDAR sensor can take readings up to 40 meters, and could be used in projects ranging from self-driving cars to home security systems.
I helped out a team by taking the output of the sensor and feeding this into Python with the goal of creating real-time plots. 
I thought it might be a good opportunity to make a quick 'n' dirty video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/oAFNRyCmBFI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

The data comes from a C file, and is piped into the Python code below:

{% highlight python %}
import matplotlib.pyplot as plt
import math
import re


##plot angle and distance on polar plot
def plotter(new_angle, new_distance): 
    fig = plt.figure(figsize=(8,8))
    angle = math.radians(new_angle)
    ax = fig.add_subplot(111, projection='polar')
    ax.set_theta_zero_location('N')
    ax.set_theta_direction(-1)
    ax.scatter(angle, distance, cmap='hsv', alpha=0.75)
    
##reading file from pipe input
try:
    creader = open('/home/stem/Stem/datadump', 'r') #ENTER FILE
except IOError:
    print('The file does not exist')
else:
    print("File exists!")    
    info = creader.read()
    info = re.split ('A|D|\n', info)
    angle, distance = float(info[1]), int (info[2])
    plotter(angle, distance)
{% endhighlight %}

We noticed that the plots don't quite match the environment, so we'll be applying Kalman filtering to smooth the data. 
A future implementation will be to calculate the velocity of moving objects in the environment and then connecting this all up to an embedded device.
