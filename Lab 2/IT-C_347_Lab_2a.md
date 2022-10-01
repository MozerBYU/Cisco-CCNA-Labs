# IT-C 347 Lab 2a
### *Conceptual & Practical Lab - Ethernet Patch Cable*
## Introduction

Regardless if you’re Helpdesk, System Administration, Network Engineer, etc. At some point in your career you’ll have the opportunity to create an ethernet patch cable. It is a vital skill regardless of your IT/Cybersecurity position.

Before we dive into the actual mechanics of creating it. Let’s familiarize ourselves with ethernet cables for a quick second, including ethernet standards, naming conventions, duplexing, and the different standards for creating a patch cable.

## Twisted-Pair Cables

Ethernet cables, also common referred to as patch cables, are created with either 2 or 4 twisted-pair cables (4 or 8 wires in total). These either come in unshielded (UTP) or shielded (STP). For modern ethernet like Cat 6a or Cat 7, there is additional shielding or foil around either the wires, the sheath or both. All of those differences are shown visually below:

![UTP vs STP Ethernet Cabeling](/assets/images/lab2a/utp-vs-stp.png) 

Ethernet in general is defined within the IEEE 802.3 standard as follows:

| **IEEE Standard**	| **Name** | **Base Name** | **Speed (Mbps)** |
| :------: | :------: | :------: | :------: |
| 802.3 | Ethernet | 10Base-T	| 10 |
| 802.3u | Fast Ethernet | 100Base-T	| 100 |
| 802.3z | Gigabit Ethernet	| 1000Base-T |	1000 |
| 802.3ae	| 10-Gigabit Ethernet	| 10GBase |	10,000 |

Now something important to note about ethernet, is that each new generation is backwards compatible with previous generations of ethernet. Part of why it is the most widely adopted standard in networking. Say you have a Cat 6 cable, you can use it like you would a Cat 4 for voice. That’d be a complete waste, but you could do it.

Now as with most IEEE standards, eventually someone realized that there is a much easier naming convention then what currently exists (you think Ethernet is bad, just wait till we get to WiFi). That is where the UTP Ethernet Categories come into play. Which are as follows below for Cat 1 up to Cat 7.

![UTP Ethernet Categories](/assets/images/lab2a/utp-categories.png)

## Duplexing

Another thing that is important to note, more for historical purposes, is that ethernet is either in half-duplex or full-duplex. Simply put, half-duplex is either send or receive, while full-duplex is send and receive. 

For some historical context, back in the ancient days of the early 80s and 90s ethernet technology was still young and developing. A lot of devices were in still using half-duplex. In addition to this people were still using these archaic devices called hubs (think of a switch but super lame). Hubs were cheap for hardware, which is why they were used. How hubs work, is when the receive a packet, they forward that to all ports. And since they were mostly operating in half-duplex, packets would collide by being trying to send and receive down the same wire. As a result, things like CSMA/CD were developed (which I’m not covering). But then some smart people decided using full-duplex and switches were much better.

## Network Speed Terminology

*Note: The following applies to both coaxial, ethernet, WiFi and fiber*

When talking about how fast a given network or network connection is, the various terms are confusing, so I’m going to hopefully shed some light on how to differentiate between each of them. First, let’s go over all the terminology and their textbook definitions really quick:

-	Bandwidth
     -	Determines how fast data *theoretically* can be *transferred* across a network
     -	Measured in bits per second (bps)
-	Latency
     -	Determines how much *delay* there is in data transit from source to destination
     -	Measured in milliseconds (ms)
-	Speed
     -	Determines how fast data can be *transmitted* across a given network medium
     -	Measured in bits per second 
-	Throughput
     -	Determines how fast data *actually* was *transferred* over time
     -	Measured in bits per second 

To put all these together in a more logical sense:

-	Speed is how much data the network can handle in a *hysical sense* (factors include: networking medium/cabeling)
-	Bandwidth is how fast the network can handle the data in a *theoretical sense* (factors include: cabling, NICs, switches, routers) 
-	Throughput is how fast the network can handle the data in a *practical sense* (factors include the actual reality use of said cabling, NICs, switches and routers)
-	Latency is how fast the network and global internet handled the data in a *reality* (factors include the actual reality of your network and the global internet and how all the cabling, NICs, switches and routers, and end services dealt with said data)

If your still lost, just know like 95% of this world (who ain’t in IT or remotely technically related) lumps like most of these into speed or latency. But here is a helpful article if you so desire:

https://www.cbtnuggets.com/blog/technology/programming/network-throughput-vs-bandwidth-the-difference

## Patch Cabling Standards

Even though I mentioned all the various ethernet categories. For this class we we’ll be focusing on Cat5e (the most commonly used ethernet category today, though Cat 6 and Cat 6a are making some headway). 

Other thing to note: the connector for ethernet is commonly referred to as RJ45. In RJ45 for Cat 5e, there are two standards, namely T-568A and T-568B. You can use either when creating a Cat 5e ethernet patch cable, as long as you are consistent on both ends. They are as follows:
 
![Patch Cabeling Standards](/assets/images/lab2a/patch-cable-standards.jpg)
 
As you notice, the only different between the two is where the Green and Orange wires are. However, like I mentioned earlier **be consistent on both ends**, otherwise you get to cut off one end and re-terminate the cable. 

## Creating a Patch Cable

In order to create the patch cable we need a few things:
-	Ethernet patch cable 
-	RJ45 clips
-	Cripping tool

We’ll demonstrate this in lab time, but here is a video demonstrating how this is done. And yes, I know this video is a tad on the cringey side. But it does a fairly good job of showing you how it’s done and explaining the whole process.

https://www.youtube.com/watch?v=zpNpfO4Z628

One helpful tip is to get all your wires in place. Then trim them so that they’re all the same length before you try to crimp them.

To test if you did it right you can either use a signal tester device, or just plug it in as you would a normal ethernet cable. You’ll know you did it wrong if you run a speed test (https://speedtest.net) and you’re speeds max out at 100 Mbps. That means only 2 of your pairs are sending/receiving data. For the full Gigabit you need all 4 pairs to be working correctly. 

Now making one of these is required for the mid-term. So keep trying until you get it right. Good luck!

## Resources

-	https://en.wikipedia.org/wiki/Ethernet
-	https://study-ccna.com/ieee-ethernet-standards/
-	https://www.tripplite.com/products/ethernet-cable-types
-	https://www.warehousecables.com/how-to-make-a-cat5-patch-cable
-	https://www.youtube.com/watch?v=zpNpfO4Z628

## Credit

Image credit to FiberOpticTutorial.com, Firewall.cx, and BlogSpot.com.

Lab credits to Nathan Moser as the sole author and editor.
