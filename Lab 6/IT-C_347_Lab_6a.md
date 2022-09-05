# IT-C 347 Lab 6
### Conceptual Lab - Routers
## Introduction

Now that we have covered IP addressing, subnetting, VLANs, and switches, you are ready to learn about the wonderful world of routers and routing.

Routers are honestly very complicated. In their purest sense, all they do is route packets from one network to another. But there are a lot of underlying technologies that make routers work, and route more efficiently and route autonomously. Some of those technologies we’ll get into a little bit, but most we won’t. If you want to get really into routers, be sure to do Lab 7 and take IT-C 529 – Advanced Networking.

Despite the complexity of routers, we will dive into a fair amount of the technical details with how it handles packets with the ARP table, how basic routing works, how static routes work, what the precedence is with routing for different routes, and then we’ll go over some basic routing technologies that are good to be aware of.

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

The most redundant of all the topologies would be either ring or mesh. Especially with regards to router, mesh is fairly common. As you can guess from the name, in mesh, every node is interconnected with each other.

![Network Topology Diagrams]\(/assets/images/lab6a/network-topologies.png "Network Topology Diagram")

For our Lab we’ve been working on, in Lab 6 we’ll be implementing a Hybrid approach of Tree for routers and switches, and Star for our hosts.

If you choose to do Lab 7, we’re going to switch things up a bit amongst the routers and implement a Hybrid model of Tree + Mesh. This way we still have the structure of a Tree topology between our Core and Distribution routers and the switches that we created in Lab 6, but we get the benefits of high availability and redundancy using OSPF (don’t worry about this for now).

## How a Router Works

Now that we have covered the various network topologies, it’s time to get right into routers. 

Like I mentioned earlier, all a router does is ‘route’ or forward packets from one interface to another, much like a switch. However, it is the more elite version of a switch, in that it operates on Layer 3 and not Layer 2. As such it has unique capabilities, like being able to route across networks (including VLANs). 

A router is similar in some respects to a switch, in that when it receives a packet on a given port it will inspect the packet’s destination and source MAC addresses, however, unlike the switch, it will strip that Layer 2 information away (as at this point, it is no longer needed). After the packet has been prepared for being routed to the next router it will then add new Layer 2 information so that it will transfer properly.

## ARP Tables

As part of that process a router create data entries in a table called the ARP Table. They are similar in some respects to the CAM Tables that switches use, but they have a lot more data and more functions.

*Note: ARP Tables are similar to CAM Tables, in that they are also persistent and will survive router reboots*

## Basic Routing

## Static Routes

## Routing Precedence for Multiple Routes

## Various Routing Technologies

## Write-up Questions

-	Does your closet router/gateway know your devices MAC address?

-	Does any other router/gateway know your devices MAC address?


## Resources
-	https://computer.howstuffworks.com/router.htm
-	https://networkengineering.stackexchange.com/questions/56643/does-a-router-send-frames-or-packets

## Credit

Image credit to some people. 

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the lab.


