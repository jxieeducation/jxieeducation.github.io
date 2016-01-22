---
layout: post
category : tutorial
tags: blockchain
tagline: "Short Guide To Making Your Own Blockchain"
excerpt: Blockchain is the crypto algorithm powering bitcoin. It's essentially a universally accessible spreadsheet that everyone can add to, but that no one can edit. In this tutorial, we are going to setup a private blockchain.
---

###Blockchain: A Really short introduction

Blockchain is the crypto algorithm powering bitcoin. It's essentially a universally accessible spreadsheet that everyone can add to, but that no one can edit. 

A blockchain is made up of blocks. A block is made up of transactions. A transaction is a valid flow of money from one address to the next. And finally, miners hash block-worth of transactions and add them to the blockchain, in exchange for bitcoin rewards. 

###How to setup your own blockchain

In this tutorial, we are going to setup a private blockchain.

0. Setup Docker
1. ```docker pull jxieeducation/multichain``` - Download my ubuntu based image
2. ```docker run --name multichain1 -d -i -t jxieeducation/multichain``` - create a container as the master node
3. ```docker run --name multichain2 -d --link multichain1:multichain1 -i -t jxieeducation/multichain``` - create and link a new container, the second node, to the master
4. Now that we have 2 nodes. We can access/ssh the nodes. 
	- ```docker ps``` - show the ids of the containers running
	- ```docker attach <id-of-multichain> ``` - access the node
5. Creating our blockchain
	- ```docker attach <id-of-MULTICHAIN1>``` - go onto the master
	- ```./makeChain.sh``` - creates a blockchain called chain1
	- make note of the output ```chain1@[ip-address]:[port]```
6. Adding the second node
	- ```docker attach <id-of-MULTICHAIN2>``` - go onto the second node
	- ```multichaind chain1@[ip-address]:[port]``` - tries to connect to chain1, but the system rejects us
	- copy the output ```multichain-cli chain1 grant <HEX1> connect,receive,send```
	- go back on the master, and grant the second node permission - ```multichain-cli chain1 grant <HEX1> connect```
	- go back on the second node, connect successfully this time - ```multichaind chain1 -daemon```
7. Create some resources on the master
	- ```multichain-cli chain1 listpermissions issue``` - get ```<HEX2>``` which is the address of the master node
	- ```multichain-cli chain1 issue <HEX2> FakeCoins 1000 0.01``` - create 1000 FakeCoins, each FakeSatoshi is 0.01 FakeCoins
	- go back to the second node, verify that 1000 FakeCoins are seen across the network - ```multichain-cli chain1 listassets```
8. Transfer some FakeCoins to the second node
	- ```multichain-cli chain1 getassetbalances``` - look at our balances of FakeCoins on both nodes
	- ```multichain-cli chain1 sendassettoaddress <HEX1> FakeCoins 100``` - send 100 FakeCoins from the master node to the second node
	- ```multichain-cli chain1 getassetbalances '*' 0``` - on both nodes, look at the balance of FakeCoins

###Where to go from here?

MultiChain is a type of private blockchain, where there's no proof-of-work. Instead of proof-of-work (which is very unscalable), there are permissions and concensus amongst the nodes. [Here](http://www.multichain.com/getting-started/) for more details on using MultiChain.
