# IT-C 347 Lab 5a
### *Conceptual Lab - VLANs*
## Introduction

VLANs, super useful, but dang, can they be confusing at times. As we go through this lab you’ll learn why VLANs are essential for any network and why they will make your life in networking much easier in the long run (no promises in the short run). But first, we need to delve into what is a VLAN, why they were created in the first place and some technical details of VLANs. However, we need to a do a brief review of the OSI Model.

## OSI Model

![OSI Model](/assets/images/lab5a/osi_model.png "OSI Model")
 
## What is a VLAN?

But just what is a VLAN? A VLAN stands for a Virtual Local Area Network. They reside as a network on-top of an existing LAN. Think of it as a subnetwork to a greater network. It operates on Layer 2 at a switch level, and Layer 3 at a router level. The entire purpose of a VLAN is separate/segregate a physical network into smaller, more manageable networks. 

## Reasons for a VLAN

VLANs were created to logically divide a physical network into smaller subnetworks for a few reasons:

-	First, to restrict broadcast domains
-	Second, to segregate the network by partitioning it logically based on what host(s) need to talk to what host(s), device characteristics (DMZ, VoIP, Management, etc), or other divisions
-	Third, to allow for ease of network administration, including applying network security policies

From a security perspective, VLANs are nice as they allow you to limit what host(s) can talk to what host(s) without the use of firewall rules (though, note that you can tie those together for greater control). 

However, from a networking perspective, VLANs allow for greater network management, as you can logically divide your physical network. Additionally, VLANs significantly reduce broadcast domains, which is an essential characteristic of larger corporate networks. A broadcast domain is a network in which every device receives the broadcast traffic of the other devices in the domain. In other works, each device in a broadcast domain can reach each other directly.

A good way to think about this, think of a home network of roughly 20 or so devices all connected to the same basic wifi/router combo device on a /24 network. All those devices can talk to each other directly. We’ll get more into this with later labs, but every time a device connects to a network or is trying to contact a different device, it sends broadcast message to find it. In our broadcast domain, every device is receiving these messages. In our home network scenario, this isn’t an issue, because we only have 20 or so devices.

Let’s change our scenario to a large corporation with 10,000 devices. Devices are constantly connecting and are sending broadcast messages to find and talk to different devices. As you can imagine, even if only 2,000 of these devices are sending broadcast messages, the network will very quickly become oversaturated with traffic. Now expand this to like Google for instance, with over 100,000 devices. If you don’t restrict the broadcast domains, you will have a serious issue with all the traffic and it will grind your network to a halt from traffic congestion. 

For a more visual representation of what I’m talking about, see the video below:

[VLAN YouTube Video](https://www.youtube.com/watch?v=jC6MJTh9fRE)

## Technical Details of VLANs

Any traffic traversing a given network is either untagged or tagged. For traffic in a given VLAN, we referred to that traffic as VLAN tagged. VLANs tagging is part of the IEEE 802.1Q specification, which defines VLAN tagging on ethernet frames as well as procedures on bridges, switches and routers for dealing with said frames. To better understand how VLAN tagging works, we’ll dive into the complex world of Ethernet Frames.

## Ethernet Frames

The following is a brief overview of ethernet frames. For every packet that goes over a network, they are encapsulated in frames, known as ethernet frames. These frames range from a minimum of 64 bytes to 1518 bytes. That size was set due to physical constraints at the time of 10Base5 media.
Note: frames larger than 1518 bytes do exist. They are often referred to as jumbo frames, but they are rare and won’t be covered much, but can go up to 9022 bytes in length.
An Ethernet frame contains three essential parts:

1)	An Ethernet header (Preamble, SFD, Destination, Source, and Type)
2)	Encapsulated data (Data and Pad)
3)	An Ethernet trailer (FCS).

Those three parts are as follows:

-	7-byte Preamble field: Layer 1 information of alternating 1s and 0s to help a device recognize an incoming packet
-	6-byte Destination MAC address field
-	6-byte Source MAC address field
-	4-byte 802.1Q VLAN Tag (if used)
-	4-byte 802.1AD VLAN Tag (if used)
-	2-byte Type field
-	Up to 1500-bytes Data field: Payload information
-	Varying size CRC field: Error Correction Information
-	4 byte FCS field: Frame Check
 
[Ethernet Frame](/assets/images/lab5a/ethernet_frame.png "Ethernet Frame")
 
802.1Q also defines that in a given domain you can have 4096 VLANs. As you can imagine, many large enterprises, like Google, Microsoft or Amazon, have the need for way more than 4096 VLANS, which is where 802.1AD comes in (this is covered more in depth in the Advanced Networking class, and will not be covered in this class). Suffice to say it allows for 4096 * 4096 VLANs in a given domain.

## Types of VLANs

There are generally 3 main types of VLANs

-	Static or Port-based: which are allocated based on the physical switch port the device is connected to
-	Dynamic: which are allocated based on physical device characteristics and sometimes an associated user profile (such as 802.1x)
-	Protocol: which are allocated based on what protocol is being used

ADD MORE HERE
## How a VLAN works

Say we have a given network, with a few devices connected to a Layer 2 switch. Where we have 2 devices in VLAN 10, 2 devices in VLAN 20 and 2 devices that are not in any VLAN. What happens when each of these devices sends out a broadcast message?
For devices within the same VLAN, they are permitted to talk amongst each other freely without the switch needing Layer 3 (routing) capabilities or having to be connected to a router (you will see this first-hand in Lab 6.
Therefore, if one of those devices in VLAN 10 wants to talk to one of the devices in VLAN 20, we will run into a problem in our current network configuration. Cross-VLAN talk requires a switch to be either: a) Layer 3 capable, or b) connected to a router (which is Layer 3 capable). 

## D*efault* VLAN
Now, what about our 2 devices that are not in any VLAN, what happens when they try to talk to any other device (either in VLAN 10 or VLAN 20)? By default, every switch automatically tags every packet received on a switch port that is not defined by a VLAN with the tag of the designated default VLAN. The default VLAN on every switch, unless changed, is VLAN 1. 
Now, why is this a security concern/network administration issue?
Since the default VLAN is VLAN 1, unless changed. Any traffic that is untagged will be on that VLAN. Say you forgot this and set your management VLAN as VLAN 1, now any untagged packet will be able traverse your management VLAN.
## *Native* VLAN

Now brief hardware thing related to switches and routers. In networking the link connecting a router to a switch is often referred to as either an uplink (going from the switch up to the router) or downlink (going from the router down to the switch). This is where native VLAN comes in. That link is known as a trunk link and as such it will have all VLANs traverse it. We’ll dive more into this feature when we get to Lab 6.

## VLANs and Subnetting

This is where all that subnetting practice ties it. As subnetting is what allows us to implement our VLANs. It doesn’t matter what VLAN you assign to a give network. But for ease of understanding try to keep it to somewhat reasonable and consistent. For example, say you have designated your IoT network to have VLAN 100. It would be fairly reasonable then to set that network with the 10.0.100.0/24 network.

## VLAN Practice

Note: The following questions are all for a 10.0.0.0/16 network

*Firewall Rules + Zones (DMZ, etc)*

## Write-up Questions
-	What networking problem are VLANs designed to solve?

-	Give some example VLANs you would create (name and function)?

-	Why is default VLAN 1 a security issue?

-	What 3 essential things comprise an ethernet frame?

## Resources
-	https://www.techtarget.com/searchnetworking/definition/virtual-LAN
-	https://standards.ieee.org/ieee/802.1Q/6844/
-	https://www.youtube.com/watch?app=desktop&v=MmwF1oHOvmg

## Vocab Glossary
-	Broadcast Domain: Is the portion of a network sharing the same layer 2 segment. Broadcast messages from hosts are sent to every port in their broadcast domain, thus hosts inside a broadcast domain can reach each other directly
-	Ethernet Frame: An Ethernet frame contains three parts: an Ethernet header (Preamble, SFD, Destination, Source, and Type), Encapsulated data (Data and Pad), and an Ethernet trailer (FCS)
-	802.1Q: IEEE Standard that defines VLAN tagging for ethernet frames
-	802.1AD: IEEE Amendment to 802.1Q that defines nested VLAN tagging for ethernet frames, thereby doubling the initial capacity. This is also known as VLAN stacking or QinQ (in reference to 802.1Q)

## Credit
Image credit to NetMgmt.WordPress.com and someone else.
