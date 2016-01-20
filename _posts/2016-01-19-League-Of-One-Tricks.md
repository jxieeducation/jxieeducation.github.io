---
layout: post
category : paper
tags: visualization
tagline: "Patch 5.4, 5.5 One Trick Analysis"
---

###League of One Tricks

I recently read a [blogpost](https://kwtrnka.wordpress.com/2016/01/15/gains-from-deep-learning/) by Keith Trnka. Keith is using some basic neuronetworks to predict match outcomes in League of Legends. He conveniently included some great [datasets](https://kwtrnka.wordpress.com/2015/09/21/bigger-league-of-legends-data-set/), which I played around with. 

As a one-trick [Nasus player](http://na.op.gg/summoner/userName=treechoper), I am really really interested in the at of the one-trick. This post contains some basic visualizations of the best and worst one-trick champions to carry with, across patch 5.4 and 5.5. The 5.4 to 5.5 [patch](http://na.leagueoflegends.com/en/news/game-updates/patch/patch-55-notes) is where Cinderhulk and the League of Tanks are first introduced.

---

###Defining Ability to Carry 

I measure someone's one-trick-ness by how exclusively someone plays a champion. 

$X_{PercentGames,Champion} = \dfrac{Number\,of\,Games\,Played_{Champion}}{\sum Number\,of\,Games_{Champion}}$

I then measure one's ability to carry by the Pearson Correlation between one's one-trick-ness and their win rate on the champion.

$ CarryPotential_{Champion} = Pearson(X_{PercentGames,Champion}, Pr(W)_{Champion})$

Simply put, Pearson Correlation is a measure of the direction of change of x in relation to y. 

$Pearson(X, Y) = \dfrac{Cov(X, Y)}{Var(X) * Var(Y)}$

After calculations of across around 500,000 players, I am able to rank champions in terms of how possible it is for one-tricks to carry on them.
![lol_pearson_screen]({{site.imgrepo}}/lol_pearson_screen.png)

###Some Statistics On One-Tricks

![lol_best_54_one_trick]({{site.imgrepo}}/lol_best_54_one_trick.png)
(Rengar ...)



![lol_worst_54_one_trick]({{site.imgrepo}}/lol_worst_54_one_trick.png)
(RIP Sona)



![lol_best_55_one_trick]({{site.imgrepo}}/lol_best_55_one_trick.png)
(Azir is probably the most popular control mage by S5 MSI)



![lol_worst_55_one_trick]({{site.imgrepo}}/lol_worst_55_one_trick.png)
(RIP Ashe . . . . . . AND Sona)



###Interesting Stats on the Patch Change
![lol_most_nerfed_one_trick]({{site.imgrepo}}/lol_most_nerfed_one_trick.png)

Let's understand why Rito made it hard for these one-tricks to carry:
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

Some thoughts on the types of champions that appear here:
* Invisible champions that can be abused in soloqueue
* Strong burst mages from Patch 5.4
* Newest released champions that Rito did not nerf yet from late S4 and early S5
