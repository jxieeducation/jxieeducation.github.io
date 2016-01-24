---
layout: post
category : paper
tags: visualization, anomalydetection
tagline: "Big short Anomaly Detection"
excerpt: I recently saw the Big Short with coworkers. And man, I am inspired to learn more about finance and investing. I spent some time figuring out the effects of the movie on Wikipedia. Here are some visualizations of the view counts for Wikipedia pages from the 2000s to December 31, 2015.


---

###The Big Short
I recently saw the [movie](https://en.wikipedia.org/wiki/The_Big_Short_(film)) with coworkers. And man, I am inspired to learn more about finance and investing. Ok, back to my main point, since I think very highly of the movie, I spent some time figuring out the effects of the movie on Wikipedia.

###Wikipedia Page Count
Here are some visualizations of the view counts for Wikipedia pages from the 2000s to December 31, 2015.

**[The Big Short (film)](https://en.wikipedia.org/wiki/The_Big_Short_(film))**
![traffic of movie page]({{site.imgrepo}}/bigshort_bigshortmovie.png)

**[The Big Short (book)](https://en.wikipedia.org/wiki/The_Big_Short)**
![traffic of book page]({{site.imgrepo}}/bigshort_bigshortbook.png)

###So did people actually learn anything from the movie?

**[CDO (The financial paradigm that broke everything)](https://en.wikipedia.org/wiki/Collateralized_debt_obligation)**
![traffic of cdo page]({{site.imgrepo}}/bigshort_cdo_ggplot.png)

**Results of running anomaly detection (Seasonal Hybrid ESD)**
![traffic of cdo anomaly]({{site.imgrepo}}/bigshort_cdo_anomaly.png)


**[Michael Burry (The protagonist of The Big Short))](https://en.wikipedia.org/wiki/Michael_Burry)**
![traffic of burry page]({{site.imgrepo}}/bigshort_mburry_ggplot.png)

**Results of running anomaly detection (Seasonal Hybrid ESD)**
![traffic of burry anomaly]({{site.imgrepo}}/bigshort_mburry_anomaly.png)

###Bonus: Effects of the movie on the people 

**The [investor](https://en.wikipedia.org/wiki/Steve_Eisman) aka Mark Baum (My favorite character)**
![traffic of baum]({{site.imgrepo}}/bigshort_mbaum.png)

**Ben The Retired Weirdo (played by Brad Pitt)**
![traffic of bpitt]({{site.imgrepo}}/bigshort_bpitt.png)
![movies of bpitt]({{site.imgrepo}}/bigshort_pitt_movies.png)
