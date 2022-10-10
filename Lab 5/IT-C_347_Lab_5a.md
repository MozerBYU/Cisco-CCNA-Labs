# IT-C 347 Lab 5a
### *Conceptual Lab - VLANs*
## Introduction

VLANs, super useful, but dang, can they be confusing at times. As we go through this lab, you’ll learn why VLANs are essential for any network and why they will make your life in networking much easier in the long run (no promises in the short run). But first, we need to delve into what is a VLAN, why they were created in the first place and some technical details of VLANs. 

## What is a VLAN?

But just what is a VLAN? A VLAN stands for a Virtual Local Area Network. They are defined in RFC 3069, and reside as a network on-top of an existing LAN. Think of it as a subnetwork to a greater network. It operates on Layer 2 at a switch level, and Layer 3 at a router level. The entire purpose of a VLAN is separate/segregate a physical network into smaller, more manageable networks. 

## Reasons for a VLAN

VLANs were created to logically divide a physical network into smaller subnetworks for a few reasons:

-	First, to restrict broadcast domains
-	Second, to segregate the network by partitioning it logically based on what host(s) need to talk to what host(s), device characteristics (DMZ, VoIP, Management, etc), or other divisions
-	Third, to allow for ease of network administration, including applying network security policies

From a security perspective, VLANs are nice as they allow you to limit what host(s) can talk to what host(s) without the use of firewall rules (though, note that you can tie those together for greater control). 

However, from a networking perspective, VLANs allow for greater network management, as you can logically divide your physical network. Additionally, VLANs significantly reduce broadcast domains, which is an essential characteristic of larger corporate networks. A broadcast domain is a network in which every device receives the broadcast traffic of the other devices in the domain. In other works, each device in a broadcast domain can reach each other directly.

A good way to think about this, think of a home network of roughly 20 or so devices all connected to the same basic wifi/router combo device on a /24 network. All those devices can talk to each other directly. We’ll get more into this with later labs, but every time a device connects to a network or is trying to contact a different device, it sends broadcast message to find it. In our broadcast domain, every device is receiving these messages. In our home network scenario, this isn’t an issue, because we only have 20 or so devices.

Let’s change our scenario to a large corporation with 10,000 devices. Devices are constantly connecting and are sending broadcast messages to find and talk to different devices. As you can imagine, even if only 2,000 of these devices are sending broadcast messages, the network will very quickly become oversaturated with traffic. Now expand this to like Google for instance, with over 100,000 devices. If you don’t restrict the broadcast domains, you will have a serious issue with all the traffic and it will grind your network to a halt from traffic congestion.

![Network Broadcast with VLANs](/assets/images/lab5a/network-broadcast-in-vlan.jpg)

For a more visual representation of what I’m talking about, see the video below:

https://www.youtube.com/watch?v=jC6MJTh9fRE

## Types of VLANs

There are generally 3 main types of VLANs:

-	Static or Port-based: which are allocated based on the physical switch port the device is connected to
-	Dynamic: which are allocated based on physical device characteristics and sometimes an associated user profile (such as 802.1X)
-	Protocol: which are allocated based on what protocol is being used

The most common amongst each of these are port-based VLANs. That is because often you will have a dedicated ethernet line from a switch to a given device on the network, and it only needs that one VLAN.

Dynamic-based VLANs are commonly used in newer enterprise networks and especially in wireless networks, as VLANs can be assigned based on a user-level rather than a device-level.

Protocol-based are extremely uncommon as they were based on IP addresses (but those can be easily spoofed, presenting a security risk). Additionally, with the high usage of DHCP in large and small networks, it negates the purpose of doing IP-based VLANs as they will change all the time.

## Technical Details of VLANs

Any traffic traversing a given network is either untagged or tagged. For traffic in a given VLAN, we referred to that traffic as VLAN tagged. VLANs tagging is part of the IEEE 802.1Q specification, which defines VLAN tagging on ethernet frames as well as procedures on bridges, switches and routers for dealing with said frames. 

Within that 802.1Q specification, is the designation that there is 4096 VLANs in a given domain. That number is fixed as is it determined by 12 bits within the VLAN tag. Now, for us or a small business 4096 VLANs seems extremely excessive. However, to a large organization like BYU or Google, they can use up all those VLAN pretty quickly and trust me they do. Now, for extremely large enterprises like Google, Microsoft or Amazon, 4096 VLANs is simply not enough for everything they need. This is where IEEE 802.1AD specification comes in. 

802.1AD is an amendment added to 801.1Q to address the need of more VLANs. We aren’t going to cover much about 801.1AD in this class as it will be covered more in depth in the Advanced Networking class. Suffice to say it allows for 4096 * 4096 VLANs in a given domain, which equates to 16,777,216 VLANs in a given domain. Don’t ask me why you’d need 16 Million VLANs, but then again I’m not Google, Azure or AWS.

## Ethernet Frames and VLANs

To better explain VLAN tagging we’re going to recall some information about Ethernet frames.

When a switch receives a frame from a device, in a port-based implementation, the switch will go in and modify the received frame’s header and insert the VLAN tag for that given VLAN.

The following is a very detailed visual explanation of the differences between a traditional ethernet frame and one with VLAN Tags:
 
![Detailed Ethernet Frame with VLAN Tags](/assets/images/lab5a/detailed-frame-with-vlans.jpg)
 
The following is an example of 802.1AD and how that frame looks:

![Ethernet Frame with 802.1AD VLAN Tags](/assets/images/lab5a/frame-with-802.1ad-vlans.png)
 
Recall from Lab 4a, that ethernet frames range in size from 64 bytes to 1518 bytes. In the case of VLAN tagged frames, that is incorrect. As the tag is 4 bytes for 802.1Q and 8 bytes for 802.1AD, those ethernet frames are increased in size to 1522 bytes and 1526 bytes, respectively.

*Note: with regards to when a switch receives a frame, it will also add the VLAN information to the CAM table for the device it originated from.*

## How a VLAN Works

Say we have a given network, with a few devices connected to a Layer 2 switch. Where we have 2 devices in VLAN 10, 2 devices in VLAN 20 and 2 devices that are not in any VLAN. What happens when each of these devices sends out a broadcast message?

For devices within the same VLAN, they are permitted to talk amongst each other freely without the switch needing Layer 3 (routing) capabilities or having to be connected to a router (you will see this first-hand in Lab 6.

Therefore, if one of those devices in VLAN 10 wants to talk to one of the devices in VLAN 20, we will run into a problem in our current network configuration. Cross-VLAN talk requires a switch to be either: a) Layer 3 capable, or b) connected to a router (which is Layer 3 capable). 

## *Default VLAN*

Now, what about our 2 devices that are not in any VLAN, what happens when they try to talk to any other device (either in VLAN 10 or VLAN 20)? By default, every switch automatically tags every packet received on a switch port that is not defined by a VLAN with the tag of the designated default VLAN. The default VLAN on every switch, unless changed, is VLAN 1. 

Now, why is this a security concern/network administration issue?

Since the default VLAN is VLAN 1, unless changed. Any traffic that is untagged will be on that VLAN. Say you forgot this and set your management VLAN as VLAN 1, now any untagged packet will be able traverse your management VLAN.

## *Native VLAN*

Now brief hardware thing related to switches and routers. In networking the link connecting a router to a switch is often referred to as either an uplink (going from the switch up to the router) or downlink (going from the router down to the switch). This is where native VLAN comes in. That link is known as a trunk link and as such it will have all VLANs traverse it. We’ll dive more into this feature when we get to Lab 6.

## VLANs and Subnetting

As a quick review, VLANs and Subnetting are very similar. They both are used to limit/segregate broadcast domains. But you're probably wondering, if they both are used to for the same function, why have both? Put simply:

- Subnets separate networks physically
- VLANs separate networks virtually or logically

Now in small business environments where you have very few VLANs, you can certainly connect the two so that a physical network is logical network. For example, say you had an IoT network on VLAN 100, you could set a subnet of 10.0.100.0/24. However, in large enterprise environments (such as BYU or AWS) that is highly impractical, as you can have thousands or millions of VLANs (as we just covered). In large enterprises IP address conservation is very important if they are a sole IPv4 network (as many still are). So association a given VLAN with a whole subnet, just isn't practical. 

So in industry how you setup you're network will vary, and will be dependent on the network size, complexity, security controls and various other factors.

Below is a video with an easy explanation of the difference between the two with visuals:

https://www.youtube.com/watch?v=6_giEv20En0

## Write-up Questions?

- How many VLANs can exist in a given local area network?

- How many VLANs can exist in that same network under 802.1AD?

-	What networking problem are VLANs designed to solve?

-	Give some example VLANs you would create (name and function)?

-	Why is default VLAN 1 a security issue?

-	How do subnets and VLANs correlate? How are the different?

## Resources

-	https://www.techtarget.com/searchnetworking/definition/virtual-LAN
-	https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=video&cd=&cad=rja&uact=8&ved=2ahUKEwi76u6rt8_5AhWKLEQIHWpSAAgQtwJ6BAgSEAI&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DkPOvDbHyxn8&usg=AOvVaw3upDLCgljGBC3mC0eDNnMm
-	https://www.youtube.com/watch?app=desktop&v=MmwF1oHOvmg

## Credit

Image credit to NetMgmt, WordPress.com and someone else.

Lab credit to Nathan Moser as the sole author and editor.

Lab credits to Nathan Moser as the sole author and editor, and to Bryan Wood for the structure and concepts of the labs.
