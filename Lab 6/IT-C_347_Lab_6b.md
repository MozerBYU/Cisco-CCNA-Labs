# IT-C 347 Lab 6b
### *Practical Lab – Routers*
## Introduction

Now that you have learned a brief understanding of routers and how they work, it's time you get to set them up.

For this next section, we’re going to focus on setting up our lab so that it looks like the following:
 
![Lab 6 Completed](/assets/images/gns3/Lab-6.png)

For this lab, you need to set up 2 Core Routers, connect them to your 2 Distribution Routers, and then set up static routes across for each of your routers. You will do this for each of the respective subnets, that require it (don't forget about your un-routable VLAN). Depending on how you set up your subnets and VLANs, your static routes will vary.

## Conceptual Methodology

Much like the previous lab, to help explain how to do this lab, I’m going to go over the lab from a high-level conceptual standpoint.

Additionally, like I mentinoned in the previous lab, we are building off each lab. The only exception to that is the next lab, where rather than building more infrastructure, we'll be modifying existing infrastructure to be more automated and efficient. As such, you won't touch anything you did the prior labs (3b, 4c, 5b).

The basic premise is of this lab, is we are connecting our two newly created Core Routers to the respective Distribution Routers underneath them (see above image for reference). Since our Routers operate strictly on Layer 3, we need to give each interface an IP address so that they can communicate.

Once you have all that configured, then you need to setup static routes, so that each network can talk to each other across the Core Router layer.

## Lab Setup
### *Setup Core Routers*

If you recall from Lab 4c, we setup an EtherSwitch Router template image. We will be using that image for setting up both of our Core Routers. What makes this specific router different from the one we used for the Distribution Routers, is that it has two very specific modules for routers (denoted by NM-1FE-TX).

Once we have those set in GNS3, you need to connect them to the Distribution Routers and to each other (3 links in total). As was mentioned briefly in the last lab, these are router links and can only exist on the router modules (denoted by f0/#). Each interface for these links needs an IP address and to be put in a subnet appropriate for said link. 

*Note: Remember that those links between the Distribution Routers and Core Routers are point-to-point links*

### *Setup Static Routes*

Recall the following about static routes from Lab 6a:

> In a nutshell, all a static route is, is a route that is set statically that tells one network how to get to another network, and what hops it needs to travel through on its path to said network. Now, how static routes work is each router in the path from one host network to another we’ll need to be configured with a static route and the appropriate next hop. This will need to be done for every static route.
>
> *Note: A static route is a route from **one** network to another*

In this lab you will have to configure one static route, on each router in sequence, for each destination network. Now, a point of clarification. Since we have two core routers, and subnets on both sides under each core router, you will need static routes going from one side to the other in both directions.

Below is an example of a how static routes are set up in Cisco iOS:

| Command	| Dest. Network	| Dest. Network Subnet Mask	| Next Hop IP Address |
| :------: | :------: | :------: | :------: |
| ip route	| 10.1.5.0	| 255.255.255.0	| 10.0.0.5 |\

## Troubleshooting

### *General*

General helpful commands for seeing your interfaces, their respective mode, the VLAN database, and other helpful information:

> `show int status`
> <br> `show int summary`
> <br> `show vlan-switch`
> <br> `show ip int brie`

### *Checking Routing*

Some helpful commands with troubleshooting routing issues:

> `show ip route`

Helpful commands in general that are cross-platform in troubleshooting routing issues:

> `ping` -> send an ICMP request packet to a device to see if you can talk to it
> <br> `trace` -> to run a traceroute to see where a packet gets stuck

## Pass-off

Now for pass-off I’m only looking for a few things:

-	1) you have 2 core routers (I don’t recommend more as it will make your lab overly complex, and cause you a lot of pain)
-	2) you have those core routers connected to your distribution routers and each other using point-to-point links
-	3) each host can talk within its subnet, VLAN and can talk outside it’s VLAN, and talk across each core router via static routes (with the exception of the un-routable VLAN)
-	4) for the un-routable VLAN, each host can talk to each other, but CANNOT talk to other hosts in other VLANs, but they can talk across core routers as needed (depending on your setup)

## Credit

All image credit goes to myself, compliments of the GNS3 Software.

Lab credits to Nathan Moser as the sole author and editor, and additional credits to Bryan Wood for the structure and content of the labs.
