# IT-C 347 Lab 7a
### *Conceptual – OSPF/STP*
## Introduction

Now I am briefly going to introduce two of the routing protocols I mentioned in Lab 6a, namely:

-	OSPF (Open Shortest Path First)
-	STP (Spanning Tree Protocol)

These are useful in environments where you are running multiple routers (as we we've done in Lab 6b). There are several reasons for these protocols that we’ll dive into, one of the most important is that it allows routers to communicate with each other about updates to routes automatically.

## OSPF

Now static routes are great and all, but think if you were in a large enterprise with 20 or so routers, would you want to have to set those up for each individual router? Not unless you were either a mad man or had zero idea what you were getting yourself into. Additionally, what do you do when a router dies or is getting overloaded? Do you want to manually have to go in and modify static routes to compensate? If only there was some way to automate this whole process so that it was also fault tolerant and ran in automation?

Luckily, someone else had that very thought and worked with some other smart people to create OSPF. OSPF is defined in RFC 2328 and again in RFC 5340 and stands for Open-Shortest-Path-First.

## How OSPF Works?

OSPF is a routing protocol that is part of the suite of IGP (interior gateway protocol) protocols. OSPF uses the LSR (link state routing) algorithm to construct a network topology based on the link-state information of connected routers. Based on the up or down status of those links, OSPF automatically reconfigures the network topology to best serve the network efficiently and effectively. And it does this rather quickly too.

OSPF operates pretty securely, as you can setup various authentication so that only routers you designate can join OSPF-enabled routers. This is very important as a rouge router, could send over false or malicious routing tables and cause havoc in the network.

*Note: One cool thing about OSPF, is it works for both IPv4 and IPv6 networks*

## OSPF Areas

However, there is a problem that needs to be addressed. OSPF works by recognizing a link-state change, or a topology change, and then broadcasting that information to its neighbors (or next hops). But each time a router recognizes or it told a change, it likewise tells its neighbors (and in the case it was told, it retells that information to the original router that sent that information out). 

You should hopefully see an impending problem, similar to broadcasts, where OSPF routers will be endlessly updating each other thus saturating the network. To solve this problem, OSPF Areas were developed to isolate the ‘broadcast domain’ of sorts, that OSPF routers talk in to tell each other about OSPF routing/topology updates.

Do note the difference, but it is helpful to analogize them to VLANs. In a similar way that VLANs separate a network virtually, OSPF areas separate the OSPF router network virtually.

## OSPF Area Types

Now, we need to go over the different types of OSPF areas first, as each performs a different function. However, due to complexity of some of these ares, that I will briefly mention, we're only going to focus on a few that you will need for your understanding at this point in your classes and for doing Lab 7b.

There are a few types of OSPF Areas:

-	Backbone (Area 0)
-	Regular (non-backbone)
-	Transit (non-destination, think of them like tunnels from one OSPF area to another)
-	And some others we’re not going to talk about (Stub, Totally Stubby, Not-So Stubby, Totally Not-So Stubby)

The main important ones are the Backbone and Regular OSPF areas. These are the main ones that we will be dealing with. The following are notes on these areas that are useful at this point of your network understanding:

-	OSPF Area 0 is strictly reserved for backbone networks between routers (core routers and area border routers)
-	The transit area is simply an area with two or more OSPF border routers attached and is used to pass traffic through it (aka it is not the destination for such traffic)
-	You can have a total of 4,294,967,295 OSPF areas

If you’re planning to get your CCNA, you can learn more about Stub, TSA, NSSA and TNSSA on your own time. We are only exposing you to the basics of OSPF in this lab, and therefore due to the complexity of trying to explain them, they will not be covered.

Below is an example network using OSPF areas.

![GNS3 Example OSPF Areas](/assets/images/lab7a/gns3-ospf-example-areas.png) 

The following videos are helpful in understanding OSPF and OSPF Areas.

https://www.youtube.com/watch?v=PIMnj2oqYIo

https://www.youtube.com/watch?v=CM9BlFHB3q4STP

Below is a picture of what OSPF could look like in GNS3 (we are not doing this btw, this is just an example):

![GNS3 Example OSPF Lab](/assets/images/lab7a/gns3-ospf-example-network.png)

## OSPF Router Types

Last thing I will cover in this section is the different router types within OSPF:
-	IR: Internal Router
-	BR: Border Router
-	ABR: Area Border Router
-	ASBR: Autonomous System Boundary Router

If you work to get your CCNA you will get more familiar with these. I've opted to only focus on our Core Routers for this next lab as it doesn't require a whole ton of additional setup to your completed lab in Lab 6b.
 
## STP

Next, we’ll talk about Spanning Tree Protocol. Basic premise of STP is to mitigate the issues related to network loops, either accidental or intentional. If you aren’t familiar with network loops, they are your worst nightmare as if not properly mitigated, they can take down your entire network. Before we dive into how these are created, let's define a network loop and a broadcast storm.

A network loop is when there are multiple active paths coming from the same source to the same destination. What happens is when a packet is sent out, it is duplicated and resent and resent and resent going down both active paths in a loop. It doesn't stop when it reaches its destination. As switches continually get faster and more efficient at moving packets this has become even more of a predicament for network administrators.

Now a broadcast storm can have similar effects where it causes a serious outage. This one is very self-explanatory, basically there is so much broadcast traffic that it is hindering or completely halting a network. If a network is improperly configured (aka, they don’t use VLANs as they should), you can easily have broadcast storms from everyday network traffic. If you have a network loop that problem is amplified. 

It is relatively easy to create a network loop. All you need is an ethernet cable that goes from one port on a switch to another port. If you try setting up redundant uplinks from a switch to a router and you don’t properly set up STP, you can create a network loop. This is very often caused unintentional by network or helpdesk technicians during normal business operations of helping employees get setup on the network, and they plug in an ethernet cable, believing it to go to the employee’s computer, when that ethernet cable in reality goes back to the switch. And boom, a network loop has been caused.

This is where STP comes in. Essentially, it is smart enough to recognize where potential network loops can occur (i.e. switch/router uplinks), and it can mitigate the effects of an active network loop.

Now it can get complicated as far as this is connected to routing, as there needs to be a ‘root’ STP router set, that is like the main source of information. If you don’t set this, you can have some unexpected problems arise. 

Feel free to check resources for more information about STP. We won’t be setting that up in Lab 7b, but I want you to have some exposure to it.

## Write-up Questions

-	What does OSPF stand for?

-	Why is OSPF better than static routes?

-	What problem does OSPF Areas solve?

-	What is OSPF Area 0 for?

-	What does STP stand for?

-	What problem does STP solve?

## Resources

-	https://en.wikipedia.org/wiki/Open_Shortest_Path_First
-	https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13703-8.html
-	https://www.youtube.com/watch?v=kfvJ8QVJscc
-	https://en.wikipedia.org/wiki/Spanning_Tree_Protocol
-	https://www.techtarget.com/searchnetworking/definition/spanning-tree-protocol
-	https://www.juniper.net/documentation/us/en/software/junos/stp-l2/topics/topic-map/spanning-tree-loop-protection.html

## Credits

Image credits to GNS3, Bryan Wood, Firewall.cx, and Networkel.com.

Lab credit to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the lab.
