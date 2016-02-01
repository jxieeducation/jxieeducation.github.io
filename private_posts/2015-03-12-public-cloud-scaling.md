---
layout: post
category : notes
tags: Infrastructure
tagline: "CloudOPS talk @ lithiumHQ "
---

###Intro:
* steve jobs said that “people who know what they’re talking about, don’t need PowerPoint.*”, that’s why I am using google slides
* the app is a social app that congests social data and provides customer supports
* Auto Scaling Groups, common notation (x, y) means an ASG with min X and max Y machines

###Stack:
* pre-reqs to moving into the public cloud: (VPC, DNS, yum / code repo..etc.)
* amazon region selection: rule —> hv 2+ regions, so that outage in one does not take down your system
* cloudformation: separate long-lived things (S3, ELB) with ephemeral things (apps) into separate templates.
* config mgmt: a lot of shifts in industry—> chef, puppet…etc. (chef is easier)
* regular chef or chef-solo: easy to hv teams change each others’ configs —> soon hv a community chef book and each individual teams’ chef-solo books
* private (yum) repo —> tar balls on FTP is not fun. perhaps try gopher. 
* yum-s3-repo-manager (by lithium), google on github. its a python script that all lithium uses
* how it works: place an RPM in “inbox” s3 folder and monitor process. puts anything it finds into the repo and then uploads the data back to s3. 
* build system - jenkins, con: not cross zone (US West != US East)
* use ec2-plugin in jenkins to launch instances as needed and tear them down afterwards, a lot of work done for user to save $ (joke: no one at lithium’s social net team know where the jerkin server is cuz it just shows up)
* DNS - managing binds suck. Use Route53 for internal stuff.
* MySQL - no RDS, lithium has good DBAs. want to tolerate instance and area zone failures without intervention
use MHA (from Fb) and MHA-heper to scale MySQL
* 2 AutoScalingGroups 1. master-eligible ASG (1 master, 1 read slave, 1 backup slave)  (3,3) 2. MHA group —> upon creation of stack, selection of master and MHA manager done to prevent them from being in the same area zone
* Floating IPs in AWS - problem, need cross-AreaZone IP address. DNS failover doesn’t hv crisp boundary across all hosts and takes too long
* Soln: use VPC route tables, put torte in route-tables to route 192.168.x.y/32 to specific ENI. upon failover, update existing routes to point to new ENI of the new master. update and traffic switch controlled at network layer and is instantaneous
* if we notice master in AZ1 fail, we change master to AZ2 (note group 1 and 2 are in the same region, but it’s ok, since new data is saved, need to wait for AZ1 to go up again).
* elasticsearch - (3,3) cross-AZ ASG. use AWS plugin. make sure to tune open file descriptor limits so cluster doesn’t fail easily
* zookeeper - uses netflix’s exhibitor to make bootstrapping cluster and node IDs much easier. also (3,3) ASG - does a lot of leader-election work over master-slave relationship
* note: don’t put zookeeper on ebs, put on ephemeral SSD disk, cuz it’s sensitive to IO latency
* redis - used multi-AZ elastic cache redis. to make life easier: use ElastiCache Redis
* ActiveMQ —> RabbitMQ —> ActiveMQ —> SQS
* ActiveMQ = poorly tested, RabbitMQ doesn’t work well in the long term (very sensitive to delayed connections, make Queue explode)
* switched to SQS (also buggy, but Amazon is doing it, so expecting improvement)
* java apps - the actual business app. easier because only need to worry about horizontal scalability

* security on the public cloud:
* local euphemeral disks —> can encrypt the local ephemeral disk
* EBS storage —> use —encrypted flag during AWS Cli bootstrap
scripting guides: **Bash - ppl not disciplined with whats in the bash cuz it’s so useful **Ruby: versioning can get hard and few people write ruby in DevOps community. **Python: 2->3 switch is difficult
* Fabric —> performing administrative tasks: thread / heap dumps, restarts, hotfix deploy orchestration
* Datadog -> monitoring
* PagerDuty -> email / call notification

full video: 
<a href="http://www.youtube.com/watch?feature=player_embedded&v=qQWPsR6Innc" target="_blank"><img src="http://img.youtube.com/vi/qQWPsR6Innc/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="480" height="360" border="10" /></a>
