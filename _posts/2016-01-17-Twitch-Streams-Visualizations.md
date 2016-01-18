---
layout: post
category : paper
tags: visualization
tagline: "Twitch Streams Visualization"
---

###Twitch Streams Visualization
[Twitch](http://www.twitch.tv/) is a place for video game players to share gameplay with others in real time. Being a long time follower of multiple twitch channels, I really wanted to analyze some Twitch data. Fortunately, there was already a [published dataset](http://dash.ipv6.enstb.fr/dataset/live-sessions/) for all the streams between January and April 2014. In this post, I will be sharing some findings and visualizations of twitch streams and streamers.

###1. Twitch streamers are located in the US and Europe  
This is not a big surprise. It makes sense that most of the streamers are in English speaking countries since the viewership and platform are mostly in English.

![Locations of twitch streamers]({{site.imgrepo}}/Popular_Streamer_Map.png)

###2. Twitch is extremely top heavy
In terms of viewership, 0.5% (7049 / 1536350) of the streamers get about 85% (4.46 * 10^9 / 5.23 * 10^9) of the viewership, measured in terms of the sum of unique daily viewers.

<img src="{{site.imgrepo}}/viewership_comparison.png" alt="viewership comparsion" style="width:500px;height:500px; margin-left:10%">

(left) Viewership of the top 0.5% of streamers (right) Viewership of the whole platform

###3. WingsOfDeath works his hardest on Wednesdays

[WingsOfDeath](http://www.twitch.tv/wingsofdeath) is my favorite streamer. So here's what I found when looking at his data.

![Wings stream duration]({{site.imgrepo}}/wings_stream_duration_heatmap.png)
(WingsOfDeath's stream duration heatmap - <Red / Short to Green / Long>)

- Wings likes to take Thursdays and Fridays Off
- He usually works the hardest on Wednesdays before he takes the next two days off
- As a full time streamer, he streamed 72 out of 95 (75.7%) days between January and April 2014

###4. (No Brainer Alert!!!) Stream length and max viewers are corrolated
![Wings stream viewership]({{site.imgrepo}}/wings_viewership_heatmap.png)
(WingsOfDeath's max viewership by day - <Red / Low to Green / High>)

- If we compare this graph and the one from above, it's easy to see that Wings get more max viewers when he streams more
- He also gets the most amount of viewers on Wednesdays

<img src="{{site.imgrepo}}/wings_viewers_vs_duration.png" alt="Scatterplot of duration vs max viewers" style="width:500px;height:500px; margin-left:10%">

(Scatterplot of stream duration vs max viewership, likely a linear correlation)



