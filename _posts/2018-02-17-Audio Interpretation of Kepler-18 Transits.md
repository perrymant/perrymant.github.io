---
layout: post
title: Audio Interpretation of Kepler-18 Transits
excerpt_separator: <!--more-->
---

In 2011, it was discovered that the star Kepler-18 has 3 exoplanets using the Photometric Transit method. I thought, why not try to make an audio file out of the data collected by the Kepler satellite on this light curve! <!--more-->

When the planet passes over the star, the observed intensity light will dip:
<img src="/images/Planetary_transit.png" alt="kepler-18-graphic" style="width: 800px; height=600px;" align="middle"/>

It turns out that Kepler-18 has 3 planets orbiting the star:
<img src="/images/kepler-18-graphic.jpg" alt="kepler-18-graphic" style="width: 800px; height=600px;" align="middle"/>
<br>
Image Credit: Tim Jones/McDonald Obs./UT-Austin
<br>
The light curve data is available at the [caltech.edu website](https://exoplanetarchive.ipac.caltech.edu) 
<img src="/images/Kepler-18.png" alt="kepler-18-graphic" style="width: 800px; height=600px;" align="middle"/>
<br>
Image Credit: https://exoplanetarchive.ipac.caltech.edu
<br>
Using the following code I converted the light curve data into a wave audio file:

{% highlight python %}
from scipy.io.wavfile import write as wav
import pandas

tbl = pandas.read_table('plot.tbl', comment='#', delim_whitespace=True) # open table as pandas dataframe
lc = tbl[2:].iloc[:,2][:64431]                                          # isolate column of light curve data
lc = lc.astype(str).astype(float)                                       # converting numpy array from float to strings
lcnp = lc.values                                                        # pandas.core.series.series to numpy.ndarray
rescale = lcnp * 100                                                    # increase amplitude
wav('Kepler-18.wav', 44100, rescale)                                    # create wave file
<br>
{% endhighlight %}
<br>
Here is the resulting audio file:
<audio controls loop>
  <source src="/Audio/Kepler-18.wav" type="audio/wav">
</audio>
<br>
After aplying a noise gate, I was able to isolate the clicks by removing the low amplitude noise. It's a crude method of truncating the noise, but it allows us to hear the individual transits far more clearly: 
<audio controls loop>
  <source src="/Audio/Kepler-18 NoiseGated.wav" type="audio/wav">
</audio> 
<br>
Here's a video that explains Transit Photometry in more detail:
<iframe width="800" height="600" src="https://www.youtube.com/embed/Bxl4DbCzQco" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
