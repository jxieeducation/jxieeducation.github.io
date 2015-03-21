---
layout: page
title: Jason Xie
tagline: Some thoughts on stuff
---
{% include JB/setup %}

[Notes]({{site.production_url}}/notes.html)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Reading list]({{site.production_url}}/readinglist.html)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Essays]({{site.production_url}}/essays.html)

[Github](https://github.com/jxieeducation)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Past venture](http://napkins.io/)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Patents](https://drive.google.com/folderview?id=0B1bSqZCsa0P3fi1CRzVkY053d3FrY3hZZlE4cHQ3NW40X09BVEFsdTVfcjFwUVRYU3dfNjQ&usp=sharing)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[Book](http://www.amazon.com/Unschool-Yourself-True-Learning-Ground/dp/1491219467/ref=sr_1_2?ie=UTF8&qid=1426888868&sr=8-2&keywords=unschool+yourself)

####Some funner things
    sudo make me a sandwich

* Hacker Chrome browser [theme](https://github.com/jxieeducation/Hackathon-Hacker-Chrome-Theme)
* Sightreading codebases for programming practice [src](https://github.com/jxieeducation/repo-sightread)
* Video summarization algorithm [code for a hackathon](https://github.com/jxieeducation/tl-dw)
* ATP tennis analysis from a long time ago [articles](http://www.sportskeeda.com/profile/jason-xie)
* TEDxRichmondHill talk on coincidences [tweets](https://twitter.com/TEDxRHill/status/367053026470543361) [talk](http://www.tedxrichmondhill.com/videos)
* An april fools joke for my roomate [game](http://diegobird.paperplane.io/)
* Why I don't make [games](https://www.dropbox.com/s/vzprwvn3yegdips/rainsetup.exe?dl=0) anymore :( [eduational booklet](https://github.com/jxieeducation/Rain/blob/master/Rain%20Action%20Guide.pdf)

####Latest
{% for post in site.posts limit:3 %}  
<li>  
    <span>{{ post.date | date_to_string }}</span> &raquo;
    <a href="{{ BASE_PATH }}{{ post.url }}">  
    {{ post.title }}</a>  
</li>  
{% endfor %}  
&nbsp;
