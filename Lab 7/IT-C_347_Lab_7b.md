# IT-C 347 Lab 7b
### *Practical – OSPF*
## Introduction

Now that you’ve learned about OSPF from a conceptual standpoint (at least a brief overview of it), we’re going to copy our Lab 6b project into a new project to setup OSPF.

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
