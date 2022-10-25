# IT-C 347 Lab 7b
### *Practical – OSPF*
## Introduction

Now that you’ve learned about OSPF from a conceptual standpoint (at least a brief overview of it), we’re going to copy our Lab 6b project into a new project to setup OSPF.

## Conceptual Methodology

Much like the previous labs, to help explain how to do this lab, I’m going to go over the lab from a high-level conceptual standpoint.

Hopefully, you understand how static routes work for getting from one network to another, and how to configure them. And hopefully, either through Googling it, looking it up on YouTube or through your own experience, you understand that it would be so beyond painfully to manually configure these in a large organization, especially to re-configure them in the case of a dead link or a dead router.

There is why OSPF is great. It automates all of this for you, it is redundant by nature, and it is self-healing if a link goes down or a whole router goes down. Granted, if you're backbone routers die, you're still doomed, but we'll ignore that in this hypothetical setup.

For the lab, you're basically setting up OSPF in place of static routes. Each router needs to know what OSPF area it belongs to, and what networks are associated with what OSPF areas. For security, we're also show you how to lock down OSPF so that a rouge router doesn't take over and modify your OSPF routes.

## Prep Lab 7

We need to do a few things first to prep the lab for OSPF. First, you need to go on each router and remove any statics routes you have created. Then for each Distribution Router, you will need to add a new wired connection to each of the other Core Routers (that you are not currently connected to).

Next, you’ll want to plan our your OSPF Areas. Recall, Area 0 is reserved for the backbone link (aka the link between your Core Routers). I recommend not getting crazy complex (i.e. having Areas 0 – 4 suffices just fine).
 
![GNS3 OSPF Example](/assets/images/lab7b/gns3-ospf-example.PNG)
 
## OSPF Commands

*// Enable OSPF on router*
<br> `Router# router ospf 1`

*Note: You’ll need to repeat the following command for each network and each OSPF area*

*// Setup the OSPF Network and Area* 
<br> `Router# network <ip_address> <subnet_mask> area #`

*// Check OSPF routing between routers*
<br> `Router# show ip route`
*Note: should show ‘c x.x.x.x is directly connected’*

*Note: You’ll need to repeat the following command for each interface connected to OSPF*

*// Setup OSPF Authentication*
<br> `Router# int #/#`
<br> `Router# ip ospf authentication`
<br> `Router# ip ospf authentication-key <password>`

*// Setup Route Summarization*
<br> `Router# router ospf 1`
<br> `area # range <ip_range> <subnet mask>`

## Pass-off

-	1) you have removed your old statics routes
-	2) you have at least 3 OSPF areas (including area 0)
-	3) you can demonstrate OSPF is working
-	4) you tried to have fun (keyword is ‘tried’)

## Resources

-	https://networkel.com/advanced-ospf-configuration-example/
-	https://networklessons.com/cisco/ccna-routing-switching-icnd2-200-105/ospf-multi-area-configuration/
