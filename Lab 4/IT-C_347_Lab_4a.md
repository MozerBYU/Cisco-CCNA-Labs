# IT-C 347 Lab 4a
### *Conceptual Lab - Switches*
## Introduction

Now that you have the basics of how subnetting and VLANs work, and have built your own ethernet cabling first-hand, you’re ready for the next section, switches. Basically, the purpose of a switch is to connect segments of a network and to allow for more efficient usage of the overall network bandwidth to many clients and devices.

Before we get into the different types of switches, we’re going to review over the OSI Model really quick. Mainly we’ll be focusing on Layers 2 and 3 for the next set of labs.

## OSI Model

![OSI Model](/assets/images/lab4a/osi-model.png "OSI Model")

They main layers to focus on for the next set of labs are Layers 2 and 3.
 
## Types of Switches

There are 2, technically 3, types of networking switches that exist:

-	Unmanaged
-	Managed
    -	Layer 2
    -	Layer 3
  
Unmanaged switches are more commonly referred to as dummy switches. They are literally plug-and-play-and-then-forget devices. You plug it in, and it allows you to connect more devices to that network. It has no administrative functions or any capabilities beyond just sending packets from one device to another. Not particularly useful unless you’re just needing a way to connect more devices to a given network. But they are cheap and used quite a bit in small businesses and home networks. One thing to note is that with an unmanaged switch, it doesn’t matter what device is plugged into what port. 

Now I have managed switches split into two separate distinctions as there are Layer 2 switches and Layer 3 switches, both of which are ‘managed’ in the sense that you can console into them and configure them how you would like. Both have dedicated links for trunks ports and switch/access ports (though in some L2/L3 switches you can designate those yourself, as we will do in the next set of GNS3 labs). 

Next, we have Layer 2 switches. They are referred to as Layer 2 as they operate on Layer 2 of the OSI Model – the Data Link layer. They perform solely ‘switching’ functions (VLANs, port management, QoS, etc). 

Lastly, we have Layer 3 switches. As you’ve probably guessed, they operate on both Layers 2 and 3 of the OSI Model – both the Data Link and Network Layer. These switches are very powerful in their capabilities as they can do more than what Layer 2 switches can, but nature of the name. By being Layer 3, they have both ‘switching’ functions and ‘routing’ functions. We’ll dive more into what routing is in the Lab 6, suffice to say for now it is what makes the internet and intranet work. Without routing, none of it would work as none of the packets would know where to go.

After talking about each of those, you might wonder why I haven’t covered hubs. Well, I’ll tell you why. It’s because hubs are about the most useless piece of networking gear that exists and are so beyond outdated that if you encounter one in your job, please take the Good Samaritan initiative and replace it with a real switch. As far as disposal, no one will judge you if you take it out back behind your grand-dad’s house, get his shotgun and hit it a time or two before you cart its carcass off to recycling,

*Note: you can skip this part, it’s just a bit of a rant. If you really want to know why I think hubs are useless, head down to the “Why Hubs are Useless” section.* 

## Layer 2 vs Layer 3

Layer 2 is the Data Link layer. Everything on this layer operates by its physical address, known as its MAC address. This is where switching occurs. Where a given ethernet frame is ‘switched’ so to speak, from one port on a switch to another. A good analogy for this is Thomas the Train Engine. 

Remember this fun little picture:

![Thomas the Train at Tidmouth Sheds](/assets/images/lab4a/tidmouth-sheds.webp "Thomas the Train at Tidmouth Sheds")
 
Much like the bridge in the middle, a switch allows for trains, so to speak, to travel from one train shed to another or to other places in either the train yard or across the world. 

Layer 3, on the other hand, is the Network layer. Everything on this layer operates by its logical address, or IP address. This is where the actual routing occurs. Building off our Thomas the Train analogy. Say a given train wants to leave the train shed and go into town, in order for it to get there, it will need to come to several junction points and be routed onto different tracks in order to get where it needs to go. Think of a router like a junction point in a given city. Except, unlike the railroad, with routers there are multiple different tracks to get to a given city. The job of the router is to determine the shortest route to get to the next city. 

If that doesn’t exactly make sense, don’t worry about it. We’ll cover it more in Lab 6. For now, you just need to understand the Layer 2 is for switching and Layer 3 is for routing.

## Ethernet Frames vs Packets

Now before we get into the technical details of how switching actual works, we need to talk about Ethernet Frames and Packets. Ethernet frames are the bits/bytes of data that are sent over Layer 2, whereas packets are the bits/bytes of data sent over Layer 3. 

The following is a brief overview of ethernet frames. Ethernet frames range in size, known as the MTU or Maximum Transmission Unit, from a minimum of 64 bytes to 1518 bytes, generally. That size equates to roughly 1.5 KB, yeah, they aren’t that big. It was original set due to physical constraints at the time of 10Base5 media. But we have stuck with it as for the most part it serves the purpose of most internet traffic, and (as will be covered more in the Digital Communications class when you learn about Error Correction Coding), 1518 bytes is easier to correct if a frame or packet gets corrupted in transit than a larger one.

*Note: frames larger than 1518 bytes do exist. They are often referred to as jumbo frames, but they are rare and won’t be covered much, but can go up to 9022 bytes in length (~9 KB).*

An Ethernet frame contains three essential segments:

1)	A Header segment (Preamble, SFD, Destination, Source, and Type)
2)	A Payload segment (Data and Pad)
3)	A Trailer segment (FCS).

Those three parts are further detailed as follows:

-	7-byte Preamble field: Layer 1 information of alternating 1s and 0s to help a device recognize an incoming packet
-	6-byte Destination MAC address field
-	6-byte Source MAC address field
-	4-byte 802.1Q VLAN Tag (if used)
-	4-byte 802.1AD VLAN Tag (if used)
-	2-byte Type field
-	Up to 1500-bytes Data field: Payload information
-	4 byte FCS field: Frame Check using CRC (though not shown in the picture below)
 
## Media Access Control (MAC) Address

One quick plug about MAC Addresses and then we’ll get into the good stuff. MAC addresses, as previously mentioned a few sections up, are the physical address for a given device. That address is generally hardcoded into the NIC (Network Interface Card) of the device. However, this can be changed on some devices (known as MAC Spoofing). 

A MAC address is determined by 2 things:

-	1) Its OUI (Organizational Unique Identifier) that is given to its particular vendor
-	2) Its UAA (Universally Administered Address) this can be considered a serial number of sorts

It is comprised of 6 octets of bits, represented in Hexadecimal. Below is a good visual example:
 
![MAC Address Diagram](/assets/images/lab4a/mac-address.jpg "MAC Address Diagram")

## How a Switch Works

A switch has several different ports, either ethernet or fiber, connected to all sorts of devices (computers, servers, wireless access points, sensors, etc). In order for data to travel from one device to get to another a switch is usually required (yes, you can technically direct connect between two devices. But that isn’t particularly useful except in a few cases. Enough of you and your technicalities).

When a given device sends out an ethernet frame to a switch it arrives on a given port, the switch will go through process known as ‘Frame Forwarding’. In which the switch will take that frame and inspect it, specifically looking at the ‘Source MAC Address’ and the ‘Destination MAC Address’. It will then look in the switching table to see if both devices (source and destination) MAC addresses are in its Switching Table, known as the CAM table (Content Addressable Memory). 

If the source MAC is not in there, it will make an entry noting the MAC address of that device and the port it is coming from. If the destination MAC is not there it will then to one of two things depending on the type of switch:

-	Layer 2: it will forward that frame to all ports in an attempt to find the desired destination device
-	Layer 3: it will look in the ‘Routing Table’ to see if there is any more information regarding where it might find that device (this will be covered more in the Lab 6)

![Switch Frame Forwarding](/assets/images/lab4a/frame-forwarding.png "Switch Frame Forwarding")
 
## Why Hubs are Useless

*Note: This is not required reading. This is purely a rant about why I hate hubs.* 

Alrighty, you’ve decided you wanted my rant. Fine, here you go. Remember how I said when a frame is sent down a port, that the switch uses its switching table to know where to send it? Here’s why hubs are useless. When a hub receives that same frame down a port, it is going to send that frame out through EVERY SINGLE PORT, known as frame flooding. This will be done either unicast, multicast or through broadcast. 

Now, initially you might not think that that is all that bad. However, hubs are older technology and a lot of them aren’t equipped with full-duplex, which means they operate in half-duplex (aka I can only send or receive). Which means frame collisions occurred ALL THE FREAKING TIME. To solve this problem some people, who thought they were pretty smart created CSMA/CD. Which basically is a standard that helps hubs take time to pause occasionally so as to stop ethernet frame collisions from trying to send a frame at the same time it is receiving one.

But you know what was an infinitely better solution??? Just creating a dang switch. And yeah, now that technology has advanced a ton in the last 20 years, a Gigabit L2 switch (even managed) are pretty dirt cheap. And so, hubs have faded into complete irrelevancy. 

If you want more rants, just wait for Lab 6 when we go over Network Topologies.

## Write-up Questions

-	What does MAC stand for? (hint: your first Google Search is probably wrong)

-	What is the biggest difference between Layer 2 and Layer 3?

-	Why is MTU standard at 1518? Why hasn’t that changed?

-	What are the 3 segments of an Ethernet Frame?

-	What is the purpose of the Switching Table?

-	(Bonus question) Why are hubs practically useless?

## Resources

-	https://en.wikipedia.org/wiki/Ethernet_frame
-	https://standards.ieee.org/ieee/802.1Q/6844/
-	https://en.wikipedia.org/wiki/Maximum_transmission_unit
-	https://www.networkworld.com/article/3584876/what-is-a-network-switch-and-how-does-it-work.html
-	https://www.computernetworkingnotes.com/ccna-study-guide/how-switches-forward-frames-explained.html

## Vocabulary Glossary

-	Ethernet Frame: An Ethernet frame contains three parts: an Ethernet header (Preamble, SFD, Destination, Source, and Type), Encapsulated data (Data and Pad), and an Ethernet trailer (FCS)
-	802.1Q: IEEE Standard that defines VLAN tagging for ethernet frames
-	802.1AD: IEEE Amendment to 802.1Q that defines nested VLAN tagging for ethernet frames, thereby doubling the initial capacity. This is also known as VLAN stacking or QinQ (in reference to 802.1Q)

## Credit

Image credit to Windows Club, Thomas the Train, CompTia, and ComputerNetworkingNotes.

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the lab.

