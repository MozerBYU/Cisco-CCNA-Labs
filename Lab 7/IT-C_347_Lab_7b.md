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

Next, you’ll want to plan our your OSPF Areas. Recall, Area 0 is reserved for the backbone link (aka the link between your Core Routers). I recommend not getting crazy complex (i.e. having Areas 0 – 4 suffices just fine). Aside from Area 0, you only need 2 more Areas, (you can add more if you want, but that could get rather complex).

Below is an image example from Advanced Networking on what OSPF Areas could look like in a configuration similar to ours:
 
![GNS3 OSPF Example](/assets/images/lab7b/gns3-ospf-example.PNG)

## OSPF Commands

The following are the commands that you need to run on your Core and Distribution routers, adapting certain parts to each configuration.

- Core and Distribution routers: you will need OSPF Areas setup on each interface
- Distribution routers only: you will need OSPF Areas on each network below your router (i.e. 10.0.10.0/24)

That should look like the following in your router config files:

### *Core Routers*

![Core Router OSPF Table Config](/assets/images/lab7b/router-ospf-table.PNG)
 
### *Distribution Routers* 

![Distribution Router OSPF Table Config](/assets/images/lab7b/distro-ospf-table.PNG)

### *Commands to Run*

*// Enable OSPF on router*
<br> `Router# router ospf 1`

*Note: You can use whatever number you want here, but that number specifies which OSPF Routing Table this is (aka. it should be consistent across all your routers)

*// Setup the OSPF Network and Area* 
<br> `Router# network <ip_address> <subnet_mask> area #`

*Note: You’ll need to repeat the above command for each network interface and each network*

*// Setup OSPF Authentication*
<br> `Router# int #/#`
<br> `Router# ip ospf authentication`
<br> `Router# ip ospf authentication-key <password>`

*Note: You’ll need to repeat the above commands for each interface connected to OSPF*

*// Setup Route Summarization*
<br> `Router# router ospf 1`
<br> `area # range <ip_range> <subnet mask>`

*Note: You only need 1 route summarization.. Think of it like a default route"

## Troubleshooting

### *General*

General helpful commands for seeing your interfaces, their respective mode, the VLAN database, and other helpful information:

> `show int status`
> <br> `show int summary`
> <br> `show vlan-switch`
> <br> `show ip int brie`

### *Checking Routing Tables*

Some helpful commands with troubleshooting routing issues:

> `show ip route`
> *Note: should show ‘c x.x.x.x is directly connected’*

### *Checking OSPF Tables and Routing*

Some helful commands with troubleshooting ospf issues:

> `show ip ospf border-routers`

Helpful commands in general that are cross-platform in troubleshooting routing issues:

> `ping` -> send an ICMP request packet to a device to see if you can talk to it
> <br> `trace` -> to run a traceroute to see where a packet gets stuck

## Pass-off

-	1) you have removed your old statics routes
-	2) you have at least 3 OSPF areas (including area 0)
-	3) you can demonstrate OSPF is working
-	4) you tried to have fun (keyword is ‘tried’)

## Resources

-	https://networkel.com/advanced-ospf-configuration-example/
-	https://networklessons.com/cisco/ccna-routing-switching-icnd2-200-105/ospf-multi-area-configuration/

## Credit

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the labs.
