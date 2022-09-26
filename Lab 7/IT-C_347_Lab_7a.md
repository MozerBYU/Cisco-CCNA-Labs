# IT-C 347 Lab 7a
### *Conceptual – OSPF/STP*
## Introduction

Now I am briefly going to introduce two of these routing protocols, namely:

-	OSPF (Open Shortest Path First)
-	STP (Spanning Tree Protocol)

These are useful in environments where you are running multiple routers (as we we’ll be doing in Lab 6b). There are several reasons for these protocols that we’ll dive into, one of the most important is that it allows routers to communicate with each other about routes automatically.

## OSPF

Now static routes are great and all, but think if you were in a large enterprise with 10 routers, would you want to have to set those up for each individual router? Not unless you were either a mad man or had zero idea what you were getting yourself into. Additionally, what do you do when a router link dies? Do you want to manually have to go in and modify static routes to compensate? If only there was some way to automate this whole process that was also fault tolerant.

Luckily, someone else had that very thought and worked with some other smart people to create OSPF. OSPF is defined in RFC 2328 and again in RFC 5340. OSPF stands for Open-Shortest-Path-First.

## How OSPF Works?

OSPF is a routing protocol that is part of the suite of IGP (interior gateway protocols). OSPF uses the LSR (link state routing) algorithm to construct a network topology based on the link-state information of connected routers. Based on the up or down status of those links, OSPF automatically reconfigures the network topology to best serve the network efficiently.

OSPF operates pretty securely, as you can setup various authentication so that only routers you designate can join OSPF-enabled routers. This is very important as a rouge router, could send over false or malicious routing tables and cause havoc in the network.

*Note: One cool thing about OSPF, is it works for both IPv4 and IPv6 networks*

## OSPF Areas

However, there is a problem that needs to be addressed. OSPF works by recognizing a link-state change, or a topology change, and then broadcasting that information to its neighbors (or next hops). But each time a router recognizes or it told a change, it likewise tells its neighbors (and in the case it was told, it retells that information to the original router that sent that information out.

You should hopefully see an impending problem, similar to broadcasts, where OSPF will be endlessly updating each other thus saturating the network. To solve this problem, OSPF Areas were developed to isolate the ‘broadcast domain’ of sorts, that routers talk in to tell each other about OSPF routing/topology updates.

## OSPF Area Types

There are a few types of OSPF Areas:

-	Backbone (Area 0)
-	Regular (non-backbone)
-	Transit
-	And some others we’re not going to talk about (stub, totally stubby, not-so stubby, totally not-so stubby)

The following are notes on these areas that are useful at this point of your network understanding:

-	OSPF Area 0 is strictly reserved for backbone networks between routers (generally core routers and area border routers
-	The transit area is simply an area with two or more OSPF border routers attached and is used to pass traffic through it (aka it is not the destination for such traffic)
-	You can have a total of 4,294,967,295 OSPF Areas

If you’re planning to get your CCNA, you can learn more about stub, TSA, NSSA and TNSSA on your own time. Due to the complexity of trying to explain it here, I will not be covering it.

## OSPF Router Types

Last thing I will cover is the different router types within OSPF:
-	IR: Internal Router
-	BR: Border Router
-	ABR: Area Border Router
-	ASBR: Autonomous System Boundary Router

Below is an example network using OSPF areas.

![GNS3 Example OSPF Areas](/assets/images/lab7a/gns3-ospf-example-areas.png) 

The following videos are helpful in understanding OSPF and OSPF Areas.

https://www.youtube.com/watch?v=PIMnj2oqYIo

https://www.youtube.com/watch?v=CM9BlFHB3q4STP

Below is a picture of what OSPF could look like in GNS3 (we are not doing this btw, this is just an example):

![GNS3 Example OSPF Lab](/assets/images/lab7a/gns3-ospf-example-network.png)
 
## STP

Next, we’ll talk about Spanning Tree Protocol. 

## Resources
-	https://en.wikipedia.org/wiki/Open_Shortest_Path_First
-	https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13703-8.html
-	https://www.youtube.com/watch?v=kfvJ8QVJscc
-	https://en.wikipedia.org/wiki/Spanning_Tree_Protocol
-	https://www.techtarget.com/searchnetworking/definition/spanning-tree-protocol

Credits
Image credits to GNS3, Bryan Wood, Firewall.cx, and Networkel.com.

Lab credit to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the lab.
