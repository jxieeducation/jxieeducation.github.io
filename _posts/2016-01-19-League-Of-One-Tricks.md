---
layout: post
category : paper
tags: visualization
tagline: "Patch 5.4, 5.5 One Trick Analysis"
excerpt: As a passionate league of legends player, who only plays one champion, I am really interested in understanding the statistics of one-tricks from a quantitative perspective. This post contains some basic visualizations of the best and worst one-trick champions to carry with, across patch 5.4 and 5.5, which saw the introduction of a new game item, Cinderhulk.
---

### League of One Tricks

I recently read a [blogpost](https://kwtrnka.wordpress.com/2016/01/15/gains-from-deep-learning/) by Keith Trnka, who is using some basic neuronetworks to predict match outcomes in League of Legends. He conveniently included some great [datasets](https://kwtrnka.wordpress.com/2015/09/21/bigger-league-of-legends-data-set/), which I played around with. 

As a one-trick [Nasus player](http://na.op.gg/summoner/userName=treechoper), I am really really interested in understanding one-tricks. This post contains some basic visualizations of the best and worst one-trick champions to carry with, across [patch](http://na.leagueoflegends.com/en/news/game-updates/patch/patch-55-notes) 5.4 and 5.5, which saw the introduction of  Cinderhulk.

---

### Defining Ability to Carry 

I measure someone's one-trick-ness by how exclusively someone plays a champion. 

$X_{PercentGames,Champion} = \dfrac{Number\,of\,Games\,Played_{Champion}}{\sum Number\,of\,Games_{Champion}}$

I then measure one's ability to carry by the Pearson Correlation between one's one-trick-ness and their win rate on the champion.

$ CarryPotential_{Champion} = Pearson(X_{PercentGames,Champion}, Pr(W | Champion))$

Simply put, Pearson Correlation is a measure of the direction of change of x in relation to y. 

$Pearson(X, Y) = \dfrac{Cov(X, Y)}{Var(X) * Var(Y)}$

After calculations of across around 500,000 players, I am able to rank the champions in terms of how possible it is for one-tricks to carry on them.
![lol_pearson_screen]({{site.imgrepo}}/lol_pearson_screen.png)

### Some Statistics On One-Tricks

![lol_best_54_one_trick]({{site.imgrepo}}/lol_best_54_one_trick.png)
(Rengar ...)



![lol_worst_54_one_trick]({{site.imgrepo}}/lol_worst_54_one_trick.png)
(RIP Sona)



![lol_best_55_one_trick]({{site.imgrepo}}/lol_best_55_one_trick.png)
(Azir is probably the most popular control mage by S5 MSI)



![lol_worst_55_one_trick]({{site.imgrepo}}/lol_worst_55_one_trick.png)
(RIP Ashe . . . . . . AND Sona)



### Interesting Stats on the Patch Change
![lol_most_nerfed_one_trick]({{site.imgrepo}}/lol_most_nerfed_one_trick.png)

Some thoughts on why Patch 5.5 made it so much harder for these guys to carry:

* Elise one-tricks can't carry because Elise can't make use of Cinderhulk
* Garen is not as tanky as the other Cinderhulk tanks and gets kited
* Tristana can't deal with the tanks by mid game
* Dr. Mundo became a very underwhelming tank
* Aatrox can't use Cinderhulk <img src="http://vignette2.wikia.nocookie.net/leagueoflegends/images/2/2b/Tear_of_the_Goddess_item.png/revision/latest?cb=20130319091548" alt="tears" style="width:24px;height:24px;">
* Cassiopeia can't abuse her flat magic penetration on tanks
* Urgot can't abuse his flat armor penetration on tanks
* Gragas is like Mundo, very mediocre
* Mordekaiser just can't burst the tanks...
* Zac used to be a uber tank with cc, but now Sejuani and others simply have more cc

![lol_most_good_one_trick]({{site.imgrepo}}/lol_most_good_one_trick.png)

Some reasons why these champions are the best to carry with:

* Invisible champions can be abused in soloqueue
* Strong burst mages from (pre-) Patch 5.4
* Recently released champions that Rito did not nerf from late S4 and early S5

In other news, I hope to make high Platinum this season =)!
