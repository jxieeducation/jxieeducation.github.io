---
layout: post
category : paper
tags: word2vec, wordembedding
tagline: "Appstore Review with Word Embedding"
excerpt: Word embedding is a technique in NLP / ML where we represent words in vectors based on their semantic context. This is a demonstration of the power of word embedding using word2vec on the Android Playstore review data.
---

### Word Embedding on Appstore Review

Word embedding is a technique in NLP / ML where we represent words in vectors based on their semantic context. This is a demonstration of the power of word embedding using [word2vec](http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf) on the Android Playstore [review data](https://github.com/MarcelloLins/GooglePlayAppsCrawler).

### Quick Demo:

Here we send in a combination of words with + or - operations. Then word2vec translate the words into vectors and perform the algebraic operations to generate a resulting vector. Lastly the word2vec model would find vectors or words that are closest to the vector that we created.

There are two kinds of words, normal english words along with android app ids, like ['com.facebook.katana'](https://play.google.com/store/apps/details?id=com.facebook.katana).

```
anime + wallpaper => 
com.animepictures.stalkerg.ap
com.jb.gosms.theme.heartscandyzebra4scs 
com.hola.launcher.theme.zc14982
```

```
com.facebook.katana + picture => 
co.vine.android
com.instagram.android
com.snapchat.android
```

```
com.outfit7.talkingtom + son =>
com.oki.phonenew
au.com.penguinapps.android.babyphone
com.russpuppy.monsters
```

```
com.google.android.apps.translate + chinese =>
com.google.android.inputmethod.pinyin
com.voicetranslator.SpeakAndTranslateFree
com.croquis.biscuit
```



### Why this App Recommendation Engine is Powerful 
Let's say that I am an advertiser with a lot of consumer data.

**case 1**: I know that a customer likes the [Talking Tom Cat](https://play.google.com/store/apps/details?id=com.outfit7.talkingtom) app. And I also know that he has a young toddler. Then I can recommend the [Monsters for Toddlers](https://play.google.com/store/apps/details?id=com.russpuppy.monsters) app. 

**case 2**: You like anime and don't have a wallpaper app installed yet. Then I can recommend you the [Anime Pictures](https://play.google.com/store/apps/details?id=com.animepictures.stalkerg.ap) app which according to the playstore description "enables you to conveniently search for anime pictures and anime wallpapers."

**case 3**: Your friend is interested in the [Minecraft: Pocket Edition](https://play.google.com/store/apps/details?id=com.mojang.minecraftpe) but she doesn't want to pay the $5.99 for the game. So we simply input 'com.mojang.minecraftpe - paid' and get the [Planet of Cubes Online](https://play.google.com/store/apps/details?id=com.plabs.planetofc) app, which is free and pretty darn similar to minecraft.

### Try it yourself:

* Install gensim
* Download the app review data with mongodb `mongoexport --jsonArray --host mobiledata.bigdatacorp.com.br -u GitHubCrawlerUser -p g22LrJvULU5B -d MobileAppsData -c PlayStore_2015_11 -fields=Developer,Url,Name,Reviews --port 21766 -o android_reviews.dump`
* Clean the data [munge.py](https://github.com/jxieeducation/Quick-Data-Science-Experiments-2015/blob/master/appstore-data-analysis/munge.py)
* Train the model [wordembedding.py](https://github.com/jxieeducation/Quick-Data-Science-Experiments-2015/blob/master/appstore-data-analysis/wordembedding.py)
* Tune parameters for gensim `min_count, iter, skipgram vs cbow, negative sampling vs hierarchical softmax`
