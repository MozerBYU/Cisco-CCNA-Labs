# IT-C 347 Lab 6
### *Conceptual Lab - Routers*
## Introduction

Now that we have covered IP addressing, subnetting, VLANs, and switches, you are ready to learn about the wonderful world of routers and routing.

Routers are honestly very complicated. In their purest sense, all they do is route packets from one network to another. But there are a lot of underlying technologies that make routers work, and route more efficiently and route autonomously. Some of those technologies we’ll get into a little bit, but most we won’t. If you want to get really into routers, be sure to do Lab 7 and take IT-C 529 – Advanced Networking.

Despite the complexity of routers, we will dive into a fair amount of the technical details with how it handles packets with the ARP table, how basic routing works, how static routes work, what the precedence is with routing for different routes, and then we’ll go over some basic routing technologies that are good to be aware of.

Below is a standard image the denotes a router (useful info for Lab 6b and general).

![Router Symbol](/assets/images/lab6a/router-symbol.png)

## Network Topologies

Before we dive in into the technical details of how routers work and how basic routing works, we need to briefly review your understanding of network topologies. 

First, let’s go over the different network topology types:
-	Bus
-	Mesh
-	Ring
-	Star
-	Token-Ring
-	Tree
-	Hybrid

### *Bus Topology*

The bus topology is perhaps the worst of all the topologies, in my opinion. In a bus topology all nodes are connected to each other in one continuous line. This was common in the archaic age as it used the least number of coaxial lines to connect all nodes. However, it is highly unsecure, as each node gets the traffic of all the other nodes. Additionally, there is no redundancy. If one node goes down, each subsequent node also goes down. Likewise, if one NIC on a node went down then that node and all subsequent nodes go down.

### *Mesh Topology*

A mesh topology is more common in large enterprise environments or among ISPs for high availability and redundancy. In this setup each node is connected to all other nodes. The real only limitation of this setup is it can get quite complex if you are not using SD-WAN (software defined networking). Additionally, as you can imagine it can rack up the costs a lot for each additional node that is introduced.

### *Ring Topology*

A ring topology can be considered the upgraded version of a Bus Topology. In this setup, each node connects to each other, and wraps completely around. In this way, if a given node goes down, the subsequent nodes will change their routes of who they talk to, in order to compensate. It does have limitations though. If you have a middle node and either side of it goes down, then you have a problem. 

### *Star Topology*

The star topology is perhaps the most common, where you have one central node that everything is connected to and talks to. It is highly scalable in the sense that you can replace one of the star ends, with another central node and build off of that. It is widely used as it is more cost effective than the other topologies. 

However, it has its limitations. There is not a lot of redundancy, if that central node goes down, then all those hosts or other nodes that are connected also go down. Additionally, you have to be aware of bandwidth requirements on that node and nodes connected to it (going down).

### *Tree Topology*

A tree topology is more common in distribution and core router setups, where each node connects to other nodes which connect to one master node. However, there is no redundancy built-in. If a ‘branch’ node goes down, that has several ‘leaf’ nodes connected to it, then all those ‘leaf’ nodes go down with it. Likewise, if that master node goes down, then all nodes go down with it.

### *Hybrid Topology*

A hybrid topology is exactly as it says, a hybrid of other topologies that are spawned because of a unique scenario use case. I can’t think of any of the top of my head, but one I’ve heard of Ring + Star.

### *Redundancy*

The most redundant of all the topologies would be either ring or mesh. Especially with regards to routers, mesh is fairly common. As you can guess from the name, in mesh, every node is interconnected with each other.

![Network Topology Diagrams](/assets/images/lab6a/network-topologies.png)

For our Lab we’ve been working on, in Lab 6 we’ll be implementing a Hybrid approach of Tree for routers and switches, and Star for our hosts.

If you choose to do Lab 7, we’re going to switch things up a bit amongst the routers and implement a Hybrid model of Tree + Mesh. This way we still have the structure of a Tree topology between our Core and Distribution routers and the switches that we created in Lab 6, but we get the benefits of high availability and redundancy using OSPF (don’t worry about this for now).

## Why Bus Topologies are Useless?

*Note: This is not required reading. This is purely a rant about why everyone should hate the bus topology*

Recall my hatred of hubs...we'll at least hubs were somewhat useful at one point, especially after CSMA/CD became a thing to help stop collisions. Bus topology on the otherhand...yeah that thing is absolutely useless. Like, who was the cheapskate you was like, "Yeah, I ain't spending money on more NICs or cabeling. I'll just connect them all together. Gee, I sure hope one of these doesn't go down. Eh, not my problem". 

I get it, once upon a time in the archaic age, it was hecka expensive to have a 1 mb connection over freaking coaxial. And adding more cabling and NICs were equally as expensive. But like, this is no longer the stone age. Cat 5e 1000ft is like $50. A a 1 Gb NIC is like pennies. 

Here's some advice, if you show up to a job and you see a bus topology **anywhere** in the network...just walk right back out and start interviewing for other jobs. Reason being, that IT team has no freaking idea what they are doing.

## OSI Model Review

Recall the following information as a review of the OSI model. I want you to specifically note the which layer deals with MAC addresses and which layer deals with IP addresses.

![OSI Model Review](/assets/images/lab6a/osi-model-part-2.png)
 
## How a Router Works

Now that we have covered the various network topologies, it’s time to get right into routers. 

Like I mentioned earlier, all a router does is ‘route’ or forward packets from one interface to another, much like a switch. However, it is the more elite version of a switch, in that it operates on Layer 3 and not Layer 2. As such it has unique capabilities, like being able to route across networks (including VLANs). 

A router is similar in some respects to a switch, in that when it receives a packet on a given port it will inspect the packet’s destination and source MAC addresses, however, unlike the switch, it will strip that Layer 2 information away (as at this point, it is no longer needed). After the packet has been prepared for being routed to the next router it will then add new Layer 2 information so that it will transfer properly.

Below is an example diagram of what that looks like, from host to switch to router all the way to the destination host. Obviously, it is very simplified, but gives the basic conceptual idea of what is happening.

![Packets to Frames from Host to Router](/assets/images/lab6a/packets-to-frames.jpg) 

## How ARP Works

ARP stands for Address Resolution Protocol, and is defined in RFC 826. More or less, ARP is used as a process of mapping IPs of devices on a network with their MAC addresses. This mapping is done via ARP broadcast packets from one host to another. When a host is trying to find another host on said network, if the gateway doesn't already have an entry for said computer in its ARP Table (we'll get to that in a second), then it will send out an ARP broadcast, asking all devices who has the requested IP address and to provide the router with its MAC address. This information (the IP address and associated MAC address are cached in the ARP Table for ease of lookups in the future).

If you confused, that's ok. Here's a helpful YouTube video explanation.

[https://youtu.be/Cx7foWGm5fo?t=93](https://www.youtube.com/watch?v=tXzKjtMHgWI)

## ARP Tables

As part of that process a router create data entries in a table called the ARP Table. ARP stands for Address Resolution Protocol. It is used as a bridge of sorts between Layer 2 and Layer 3. ARP Tables are similar in some respects to the CAM Tables that switches use, but they have a lot more data in their entries and more functions. 

The main purpose of an ARP table is association between a devices MAC address and its IP address. The router will occasionally receive requests from an individual host to talk to another host via its MAC address. Either the host or router will send out an ARP request asking for the MAC address of the device with a given IP address. The ARP table on the router is populated by the requests, or when it receives packets and inspects them.

The following information is also in an ARP table entry:

-	IP Address: the IP address of the device
-	Link Layer Address: the MAC address of the device
-	Expire: a timer counting down until the entry is not longer considered up-to-date and is then flushed from the ARP table
-	Netif: the specific network interface the device is connected to

*Note: ARP Tables are similar to CAM Tables, in that they are also persistent and will survive router reboots. This is because ARP entries are stored in on-board memory on the router*

## Basic Routing

Below is a diagram of the basic decision process of a router, in what it does with a packet when that packet arrives on a given interface. 

More or less, it looks to see if the destination IP address in its ARP table, or at least if the associated subnet is in the ARP table. From there it will check if that network is directly connected to the router or if it on another router (next hop). In a last resort scenario, it will forward it onto the next hop, or it will just drop it as it has nowhere to go.

![Router Forwarding Decisions](/assets/images/lab6a/router-forwarding-decisions-edited.jpg)

Basically, the router will receive the packet, and search its ARP table to see if there is a matching entry for where that packet should go. If it ultimately can’t find a destination then it will drop the packet.

*Note: this process is different than a switch. Recall a switch will forward the packet out on all interfaces if it can find the host in the CAM table. A router on the otherhand, will drop the packet rather than forward it out on all interfaces*

## APIPA

Now, before we go over static routes, I’m quickly going to go over Automatic Private IP Addressing (APIPA). When a device is connected to a network, but unable to contact a DHCP server to get an address, it will self-assign an address in the 169.254.0.0/16 address space. 

You’re probably wondering how this is useful as 169.254.0.0 is not in any of the RFC defined Private IP ranges (10.x.x.x, 172.16.x.x or 192.168.x.x). By self-assigning itself an address, that device will show up on the network (as switches and routers will cache in in their CAM/ARP tables). However, as the IP address is not in the defined network scope, it will be un-routable by default on virtually every network on this planet (and hopefully it is, we’ll talk about security of this in a second). But what this allows is for a Network Administrator to detect a rogue device on the network, and either block it (if malicious) or hunt it down and get its network connectivity restored properly (if it is not malicious). Additionally, this could be a clue that your DHCP server just freaking died (Scenario: no new DHCP leases are being handed out, and several devices start reporting in your admin console with the IP 169.254.x.x once their DHCP leases expire). 

Now, why would you not just setup a static route, as we’re about to show you, to let these devices route properly? Well, for 1) you could have a DHCP issue or other network issues that this would hint you toward, 2) that’s insecure as heck, as any device could randomly connect (granted that’s what DHCP is for in the first place), but let’s say you hypothetically, had a pure static IP network, say your Management Network, now you have a rogue device on it that is routable, and 3) why? Just why?? Why not just go and fix the network connectivity on the device in question?

*Note: It would be considered highly bad practice to route 169.254.x.x on any network, but definitely on a corporate one. Just don’t do it*

## Static Routes

In a nutshell, all a static route is, is a route that is set statically that tells one network how to get to another network, and what hops it needs to travel through on its path to said network. Now, how static routes work is each router in the path from one host network to another we’ll need to be configured with a static route and the appropriate next hop. This will need to be done for every static route.

*Note: A static route is a route from one network to another*

Below is an example of a how static routes are setup in Cisco iOS:

| Command	| Dest. Network	| Dest. Network | Subnet Mask	| Next Hop IP Address |
| :------: | :------: | :------: | :------: | :------: |
| ip route	| 10.1.5.0	| 255.255.255.0	| 10.0.0.5 |

## Routing Precedence for Multiple Routes

Now there is very important principle that you must understand, as you work with various routing technologies (some of which we’ll briefly mention here in a second), there will be times where a router has to decided where to send a packet and it has multiple routes that it could send that packet.

Don’t get confused, it is a good thing to have multiple routes to a given target network. That increases the resiliency of our network, should a given router go down or get slowed down by other traffic. But there are some considerations when we do that, that we need to account for. 

For example, say we have some static routes setup, and we also have OSPF setup that is also providing routes for a given network. If there are multiple routes, this then begs the question, how does the router know where to send the packet? How does it choose one route over another?

This is where routing precedence comes in. From a very high-level perspective, when a router has to make a decision about which route to choose, it will choose the most specific route.

To go more in-depth about how the router chooses the most specific route, there are three main principles that govern that process:

1)	Route Specificity
2)	Administrative Distance
3)	Metric

*Note: The following definitions are taken directly from Cisco.com*

### *Route Specificity*

This is also known as ‘longest prefix matching’. This is determined by comparing the destination IP address bit-by-bit with the prefixes that exist in the entries in the routing table. The route with the prefix that has the most matching bits is the one the router will chose.

### *Administrative Distance*

It is the measure of trustworthiness of the source of the route. If a router learns about a destination from more than one routing protocol, administrative distance is compared and the preference is given to the routes with lower administrative distance. 

| Default Administrative Distances |
| :------: | :------: | :------: | :------: |
| Connected	| 0	| OSPF	| 110 |
| Static	| 1	| IS-IS	| 115 |
| EIGRP (summary route) |	5	| RIP	| 120 |
| eBGP	| 20	| EIGRP (External)	| 170 |
| EIGRP (Internal)	| 90	| iBGP	| 220 |
| IGRP	| 100 | - | - | 		

### *Metric*

It is the measure used by a given routing protocol to calculate the best path to a given destination, if it learns multiple paths to the same destination. Each routing protocol uses a different metric.

As the router receives updates to route information, it will choose the best path for a given routing protocol to a given destination, and then attempt to add that route into the routing table. The router will then decide whether or not to add that route to the routing table based on the administrative distance and metrics of the route in question.

In the case where all three of these attributes are identical, the router will load balance across all available paths using ECMP (Equal Cost Multi-Path).

If all of this is going over your head, that’s ok. I’m just giving you a high-level view of how routing precedence works. If you want to get a better explanation, I have included a video below that has a fairly good explanation:

https://www.youtube.com/watch?v=PDcwijVC4XE

## Routing Protocols

-	RIP/RIPv2 (Routing Information Protocol)
-	OSPF (Open Shortest Path First) - Covered in Lab 7
-	STP (Spanning Tree Protocol) - Covered in Lab 7
-	BGP (Border Gateway Protocol)
-	IGP (Interior Gateway Protocol)
-	EIGRP (Enhanced Interior Gateway Routing Protocol)
-	ISIS (Intermediate System-to-Intermediate System)
-	VRF (Virtual Routing and Forwarding)
-	VXLAN (Virtual Extensible LAN)
-	SD-WAN (Software Defined WAN)
-	MPLS-VPN (Multiprotocol Label Switching)
-	IPSec Tunnels

Below is a YouTube video that goes over some of these protocols and why they are used:

https://www.youtube.com/watch?v=LYE8Y-zDQa8

*Note: If you want to learn more about these protocols, be sure to take the Advanced Networking* 

## Write-up Questions

-	Does your closet router/gateway know your devices MAC address?

-	Does any other router/gateway know your devices MAC address?

-	What does ARP stand for? What is its purpose?

-	What decides routing precedence?

-	What is the Administrative Distance for OSPF?

- (Bonus Question) Who created the bus topology? Be sure to look what else they've created (extra points for @'ing them in the #it347 slack channel)

*Note: If you do @ them in the #it347 slack channel, when people get confused and starting asking you about it...say nothing*

## Resources

-	https://computer.howstuffworks.com/router.htm
-	https://networkengineering.stackexchange.com/questions/56643/does-a-router-send-frames-or-packets
-	https://www.auvik.com/franklyit/blog/what-is-an-arp-table/
-	https://www.networkworld.com/article/2750342/checking-your-arp-entries.html
-	https://www.techtarget.com/whatis/definition/Automatic-Private-IP-Addressing-APIPA
-	https://www.practicalnetworking.net/stand-alone/route-precedence-how-does-a-router-choose-its-preferred-path/
-	https://my.ine.com/Networking/courses/6758d610/ine-ccnp-rs-routing-technologies-for-pro
-	https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8651-21.html
-	https://networklessons.com/cisco/ccna-200-301/longest-prefix-match-routing

## Credit

Image credit to EduCBA, NextGenT, Cisco Press and someone else.

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the lab.
