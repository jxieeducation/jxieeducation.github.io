---
layout: post
category : notes
tagline: "SFScala talk @ Nitro"
---
{% include JB/setup %}

###First talk - Rapture
TL;DR: rapture = pseudo-dynamic, typesafe, supports typeless data

* Installing scala: (scala version 2.10 works —> 2.11 doesn’t.)
* wget http://rapture.io/snapshot.jar
* scala -cp snapshot.jar

#####Rapture is a collection of (40-6x) libraries (e.g. I/O, cryptography and JSON & XML processing), to deal with dynamic vs static world

example:
{% highlight scala linos %}
import rapture.uri._ 
import rapture.net._

val sample = uri"http://rapture.io/sample.json” /** creates a HttpUrl */

val sample = uri"http://rapture.io/sample.json” /** creates a HttpUrl */
if we do: uri”htpp://rapture.io”, need to —> import rapture.codec._
import encodings._’UTF-8’._
now when we do slurp: sample.slurp[Char] —> prints the json

import rapture.json._
this imports various json backends, e.g. Argonaut, Jackson, Jawn,…
Json.parse(src) —> works just like a normal function in a language like ruby
Although json fundamentally is typeless, rapture uses the backend libraries to make this easy, so we can program scala like a dynamic language

val json = Json.parse(src)
json.groups(0).members(1).name (this outputs undefined; not error at runtime)
more examples to illustrate that it works:
json \ "groups"
json \\ "groups"

json""" {} """
json""" {"foo" : "bar"}  """
(res# \\ "key") —> works
(res# \\ "key")(1) —> works
(res# \\ "key")(1).substring(HUGENUMBER that doesn’t exist) —> outputs: rapture.json.Json = undefined
Again, there is no exception thrown. keeps Rapture’s promise to not cause runtime errors

{% endhighlight %}

#####design philosophy: no one likes runtime exceptions, so need a solution to typeless data

#####rapture: a way to implement the potential solutions for typeless data without exceptions

#####why is this library important: 
* Scala developers love type-safety
* this is bad for typeless data like user input or JSON file
* rapture has the tools to deal with the typeless inputs
* interface is the same as a non-static language
* life = easy

###Second talk - Spark Notebook(REPL for distributed data analysis)
**REPL is the interactive CLI for Scala —> similar to ipython and ipython notebooks

* The spark notebook is browser based —> control apache spark from browser
* the interface is just like an ipython notebook, well because it is built off ipython (see https://bigsnarf.files.wordpress.com/2014/03/screen-shot-2014-03-26-at-8-56-29-pm.png)
* how it works: 
* input —> ipython parser —> scala code —> spark
* results —> js parser —> formatted via D3 and numpy

#####why is this important:
* spark notebook allows for reproducible analysis using scala and spark
* the original data (and original computer code) can be analyzed (by an independent investigator) to obtain the same results of the original study
* very difficult in data science because of the nature of machine learning
* creates a spark environment, controlled via scala, interactive via ipython
