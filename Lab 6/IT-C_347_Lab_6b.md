# IT-C 347 Lab 6b
### *Practical Lab – Routers*
## Introduction

Now that you have learned a brief understanding of routers and how they work, it's time you get to set them up.

For this next section, we’re going to focus on setting up our lab so that it looks like the following:
 
![Lab 6 Completed](/assets/images/gns3/Lab-6.png)

For this lab, you need to set up 2 Core Routers, connect them to your 2 Distribution Routers, and then set up static routes across for each of your routers. You will do this for each of the respective subnets, that require it (don't forget about your un-routable VLAN). Depending on how you set up your subnets and VLANs, your static routes will vary.

## Setup Core Routers

If you recall from Lab 4c, we setup an EtherSwitch Router template image. We will be using that image for setting up both of our Core Routers. What makes this specific router different from the one we used for the Distribution Routers, is that it has two very specific modules for routers. 

Once you have them set in GNS3 and connected to each of the Distribution Routers, there are a few things that you need to do:
-	Set an IP address on each interface that connects each router (distribution & core)
-	Enable routing on each of the core routers
-	Set up static routes on each router for each subnet that needs it (this will be specific to your individual setup)

## Note on Static Routes

Recall the following about static routes from Lab 6a:

> In a nutshell, all a static route is, is a route that is set statically that tells one network how to get to another network, and what hops it needs to travel through on its path to said network. Now, how static routes work is each router in the path from one host network to another we’ll need to be configured with a static route and the appropriate next hop. This will need to be done for every static route.
>
> *Note: A static route is a route from **one** network to another*

In this lab you will have to configure one static route, on each router in sequence, for each destination network. Now, a point of clarification. Since we have two core routers, and subnets on both sides under each core router, you will need static routes going from one side to the other in both directions.

Below is an example of a how static routes are set up in Cisco iOS:

| Command	| Dest. Network	| Dest. Network Subnet Mask	| Next Hop IP Address |
| :------: | :------: | :------: | :------: |
| ip route	| 10.1.5.0	| 255.255.255.0	| 10.0.0.5 |

## Pass-off

Now for pass-off I’m only looking for a few things:

-	1) you have 2 core routers (I don’t recommend more as it will make your lab overly complex, and cause you a lot of pain)
-	2) you have those core routers connected to your distribution routers (single links)
-	3) each host can talk within its subnet, VLAN and can talk outside it’s VLAN, and talk across each core router via static routes (with the exception of the un-routable VLAN)
-	4) for the un-routable VLAN, each host can talk to each other, but CANNOT talk to other hosts in other VLANs, but they can talk across core routers as needed (depending on your setup)

## Credit

All image credit goes to myself, compliments of the GNS3 Software.

Lab credits to Nathan Moser as the sole author and editor, and additional credits to Bryan Wood for the structure and content of the labs.

