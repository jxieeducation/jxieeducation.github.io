---
layout: post
category : notes
tags: Infrastructure
tagline: "RUXIT system architecture"
---

* RUXIT is a B2B SasS platform, which transitioned to AWS in 80 days (june 2014 - october 2014)
* 1 cluster for a large number of distinct customers. 4 clusters in total (1 on west coast, 2 on east, 1 in Europe)
* each customer is an agent that communicates with the cluster regularly 

#####overall architecture: 
* clients / agents —> elastic load balancer —> proxy —> security gate way —> server —> cassandra DB cluster
* RUXIT runs 2 clusters on the east coast —> scaled up locally for latency optimization
* uses cloudcontrol to be the head of the whole system (from provisioning to recovering)
* after cloud control layer, has a business logic layer —> applies economic optimizations that incorporates RUXIT’s data (contains Monexa, salesforce and Markete…etc.)
* challenges: AWS scaling, real time provisioning of DNS names, zero downtime without manual intervention (hard to plan beforehand e.g. for e-commcerce sites)

#####How 0 downtime is achieved: 
* over provisioning : never run above two thirds of capacity
* quarantine mode : if a server node fails, groups will quarantine this node, everyone will know to not communicate with this node anymore to reduce damage to system —> be kind to ur developers, let them sleep until morning
* rolling updates : 2/3 approach again, keep 2/3 functioning, update the 1/3 horizontally
* soft stickiness : combining data locality with transparent failover —> imagine like 3-4 layers, with many machines on each layer. if 1 route failed, the agent will try again, this time taking a new random route (this is called constant failover) —> just like constant failover, but give more probability to nodes in locality, this just optimizes the routing

#####DevOps to NoOps (how to build a NoOps team)
* autonomous operations
* feedback and transparency
* everything is production
* data-driven operations
