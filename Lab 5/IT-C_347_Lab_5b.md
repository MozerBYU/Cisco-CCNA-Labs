# IT-C 347 Lab 5b
### *Practical Lab – VLANs*
## Introduction

Now that you have learned about the conceptual and technical side of VLANs, we’re ready for the next step in our GNS3 lab, setting up VLANs with Distribution Routers.

For this next section, we’re going to focus on setting up our lab so that it looks like the following:

![Completed Lab 5](/assets/images/gns3/Lab-5.png "Completed Lab 5")

For this lab, you need to setup 2 Distribution Routers, connect them to each of your 4 switches, and then setup the VLAN SVIs on the routers.  

## Setup Distribution Routers

We'll use the same EtherSwitch image that we setup for our switches in Lab 4c to setup our Distribution Routers.

*Note: Make sure you use the EtherSwitch and not the EtherSwitchRouter or you'll have some issues.*

Once you have them set in GNS3 and connected to each of the switches there are few things that you need to do:
-	Set each port to either access or trunk mode
-	Set each access port in its corresponding VLAN
-	Create each of your VLAN interfaces
-	Setup SVIs for each routable VLAN 
-	Set IP addresses on all trunk ports and SVIs

## Note about SVIs

VLAN SVIs are used by the Cisco routers to designate a gateway for a given VLAN subnet. Put simply, a gateway is a central contact point for each host in a given subnet, that allows them to talk outside of their given subnet. In order for each of your hosts to talk outside of their VLAN, they need a gateway, to tell them how to talk to the other subnets. 

Now, don’t get confused. You don’t need a gateway for a host to talk to another host on a given subnet, as long as they are connected via switches or hubs. But you do need a gateway or router to talk to other hosts on other subnets. We’ll dive more into why this is, in the next lab on routing. 

*Note: Since SVIs make it so that a given subnet can talk to another, for your unroutable VLAN you DO NOT want an SVI. If you do make one it will then be considered routable, as it is able to talk to the other VLANs and they can talk to it.*

## Pass-off

Now for pass-off I’m only looking for a few things:
-	1) you have at least 2 distribution routers
-	2) you have at least 4 switches connected to those distribution routers. Preferably, 2 switches to each distribution router
-	3) each host can talk within its subnet, VLAN and can talk outside it’s VLAN relative to the distribution router it is connected to
-	4) for the unroutable VLAN, each host can talk to each other, but CANNOT talk to other hosts in other VLANs

## Credit

All image credit goes to myself, compliments of the GNS3 Software.

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the labs.
