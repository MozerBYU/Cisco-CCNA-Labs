# IT-C 347 Lab 3a
### *Conceptual Lab - Subnetting*
## Introduction

Subnetting is an extremely useful skill for network design, setup and troubleshooting. Before we dive in deep into subnetting, we need to first understand more about the relation between public IP addressing and private IP addressing. 

## Public vs Private IP Addressing

Public IPs are globally accessible and are defined by the IANA. A good analogy that will help out in understanding this is the following: think of Public IPs like the US mail system. Each building has a street address that defines what state and city a given building resides in, and what specific street address corresponds with that building. Like the US mail system, the IANA defines the rules that surround Public IP addressing. If they didn’t there would be mass chaos.

Private IPs are locally accessible and are defined by RFC 1918. Since they are local that means they can’t be accessed from the global internet. In fact, most routers and firewall will completely drop traffic from the global internet if it the source IP is a private IP. Going back to the above analogy, think of a Private IP like an individual apartment within an apartment complex. Take Heritage Halls for example, the Public IP would in this case be ‘Heritage Halls Building 8’, whereas a Private IP would be an individual apartment, say ‘1108’. 

## IP Routing

But you can see a problem. How do you know how to get from Heritage Halls to Helaman Halls? In real life we can use Google Maps, which will direct us what turns we need to take to get to our given destination. But how does that work in the world of the networking? This is where routing comes into play. We’ll dive more into routers in later labs, but for now note that routers are responsible for routing internet traffic across the globe. In our scenario, they are that Google Maps that tells the packets what turns they need to take, so to speak, to eventually arrive at their desired destination.

Building off the same analogy, routers can get us from one apartment building to another, but how do we get to an individual apartment within that apartment building? This is where Networking Address Translation (NAT) comes into effect. NAT is a process developed to translation Private IPs to Public IPs by modifying the IP address header of the packet while it is in transit. We’ll dive more into the specifics of this process in a later lab. 

## Exercise

If you recall from the Intro to Web Programming class, they had you run through an exercise where you identify a given device’s private IP and public IP (generally your computer). We’re going to have you do the same, to refresh your memory and solidify your skills. There are many ways to do this, I will show you the simplest method, aka the terminal shell. 

To find your public IP address, simply Google “What is my IP address?”. The following will show you how to find your private IP address.

### Windows 10

Open the Command Prompt and run “ipconfig”. You will see similar to the following: 

![Windows CLI image of ipconfig command](/assets/images/lab3a/ipconfig_win.png)

### MacOSX

Open Terminal and run “ifconfig”. You will see similar to the following:

![MacOS CLI image of ifconfig command](/assets/images/lab3a/ifconfig_mac.png)
 
### Linux (Ubuntu/Debian)

Open Terminal and run “ifconfig”. You will see similar to the following:

![Linux CLI image of ifconfig command](/assets/images/lab3a/ifconfig_linux.png)
 
## Gateways and Broadcast

Gateways are generally the 1st address in an IP range (i.e. 10.0.0.1 or 192.168.1.1). However, they can be any host within the specified IP range (i.e. 10.0.0.128). The purpose of a gateway is to act as centralized location through which network traffic is translated between one network and another. It most cases one network is a LAN and the other is a WAN.

For a lot of networks, a gateway is either a firewall or a router. Some of the gateway’s duties include: 
-	Establishing and monitoring network traffic states
-	Resetting states as need in the case of state failures (lost connections, missing or late responses, fragmented responses, etc).
-	Carrying out any NAT’ing for the internal network devices

On the technical side, gateways are responsible for translating frames and protocols to other formats, so they can be routed/forwarded to the next host in a way it understands. We’ll go over gateways more when we get to routers.

## IP Classes

IP addressing is divided into different classes: classful and classless. For public IP addressing, it resides within the classful addressing space. Consisting of 5 different classes: A, B, C, D, and E. Private IP addressing, on the otherhand, resides within the classless addressing space and uses subnetting and CIDR for designating the different IP ranges.

## Classful Addressing (Public Classes)

| **Class IPv4** | **IP Address Range**	| **# of Networks** | **# of Hosts per Network** |
| :------: | :------: | :------: | :------: |
| A |	0.0.0.0 – 127.255.255.255	| 128 | 16,777,214 |
| B	| 128.0.0.0 – 191.255.255.255	| 16,382 | 65,534 |
| C	| 192.0.0.0 – 223.255.255.255	| 2,097,152 | 254 |
| D	| 224.0.0.0 – 239.255.255.255	| - |
| E	| 240.0.0.0 – 255.255.255.255	| - |

*Note: Class D is reserved for Multicasting. And Class E is reserved for future use*

## Classless Addressing (Private Classes)

| **Class IPv4** | **IP Address Range** | **# of Hosts per Network** | **Largest CIDR** | **Subnet Mask** | **Host ID Size** | **Mask Bits** |
| :------: | :------: | :------: | :------: | :------: | :------: | :------: |
| A | 10.0.0.0 - 10.255.255.255 | 16,777,214 | /8 | 255.0.0.0 | 24 | 8 |
| B | 172.16.0.0 - 172.31.255.255 | 1,048,576 | /12 | 255.240.0.0 | 20 | 12 |
| C | 192.168.0.0 - 192.168.255.255 | 65,536 | /16 | 255.255.0.0 | 16 | 16 |

Classless IP Addressing is specifically reserved for private networks (LANs) and is defined by RFC 1597 and 1918. As such, it is not publicly routable. Most edge routers and firewalls will block inbound connections originating from these IP ranges by default as a security measure.

## Subnetting

First thing we need to understand is what is a subnet. A subnet is short for sub-network. Within a larger private network, you can have hundreds and thousands of little or large sub-networks, or subnets. But how do we define the size of an individual sub-network? And how do we differentiate between one sub-network and another? This is where subnet ids and Classless Inter-Domain Routing (CIDR) come in. Below is an illustration of how a subnet id is defined.

![Subnet ID Illustration](/assets/images/lab3a/subnet_id.png)
 
The network prefix is what defines the network address. The subnet id defines what subnet the given network resides in, and the host id defines which host it is. For example, take a 10.0.x.x network and say we want to have a subnet with the subnet id of 3, our network would be 10.0.3.x. If we put a host on the that subnet with a host id of 2 it would have the IP address of 10.0.3.2 on the 10.0.3.0 subnet. 

Now you have a basic understanding of how to define a subnet and the IP addressing of an individual device within that subnet. You also have a basic understanding of how private IP networks are defined with regards to their subnet id. But before we dive into how we separate a larger private network, into smaller sub-networks using the CIDR, we need to brief touch on how public networks are defined with regards to their network id.

![Network and Host ID](/assets/images/lab3a/network_and_host_id.gif)

# Subnet Binary Math

I was going to write out how to do all this, but NetworkLessons already has a very astheticly pleasing guide/tutorial demonstrating how to do this. So I've provided the following guide for your reading. Don't worry if it seems super low-level and complicated, I have a nice tool for you I'll show in a second that is extremely helpful.

https://networklessons.com/subnetting/subnetting-in-binary

Below is a helpful video explaining subnet math:

https://www.youtube.com/watch?v=s_Ntt6eTn94

*Note: I'm not going to require you to do subnet binary math in these labs. But you need to have a general conceptual understanding of how we derive a given IP address, Subnet or Subnet mask*

## CIDR Notation

Below is a table of all CIDR notation from a /0 subnet all the way to a /32 subnet. For each subnet, there is the associated subnet mask, how many addresses and what the wildcard is.

| **CIDR Notation Prefix** | **Subnet Mask** | **# of Hosts** |	**Wildcard Address** |
| :------: | :------: | :------: | :------: |
|/0	| 0.0.0.0	| 4,294,967,296	| 255.255.255.255 |
| /1	| 128.0.0.0	| 2,147,483,648	| 127.255.255.255 |
| /2	| 192.0.0.0	| 1,073,741,824	| 63.255.255.255 |
| /3	| 224.0.0.0	| 536,870,912	| 31.255.255.255 |
| /4	| 240.0.0.0	| 268,435,456	| 15.255.255.255 |
| /5	| 248.0.0.0	| 134,217,728	| 7.255.255.255 |
| /6	| 252.0.0.0	| 67,108,864 | 3.255.255.255 |
| /7	| 254.0.0.0	| 33,554,432 | 1.255.255.255 |
| /8	| 255.0.0.0	| 16,777,216 | 0.255.255.255 |
| /9	| 255.128.0.0	| 8,388,608	| 0.127.255.255 |
| /10	| 255.192.0.0	| 4,194,304	| 0.63.255.255 |
| /11	| 255.224.0.0	| 2,097,152	| 0.31.255.255 |
| /12	| 255.240.0.0	| 1,048,576	| 0.15.255.255 |
| /13	| 255.248.0.0	| 524,288	| 0.7.255.255 |
| /14	| 255.252.0.0	| 262,144	| 0.3.255.255 |
| /15 |	255.254.0.0	| 131,072	| 0.1.255.255 |
| /16	| 255.255.0.0	| 65,536	| 0.0.255.255 |
| /17	| 255.255.128.0	| 32,768	| 0.0.127.255 |
| /18	| 255.255.192.0	| 16,384	| 0.0.63.255 |
| /19	| 255.255.224.0	| 8,192	| 0.0.31.255 |
| /20	| 255.255.240.0	| 4,096	| 0.0.15.255 |
| /21	| 255.255.248.0	| 2,048	| 0.0.7.255 |
| /22	| 255.255.252.0	| 1,024	| 0.0.3.255 |
| /23	| 255.255.254.0	| 512	| 0.0.1.255 |
| /24	| 255.255.255.0	| 256	| 0.0.0.255 |
| /25	| 255.255.255.128	| 128	| 0.0.0.127 |
| /26	| 255.255.255.192	| 64	| 0.0.0.63 |
| /27	| 255.255.255.224	| 32	| 0.0.0.31 |
| /28	| 255.255.255.240	| 16	| 0.0.0.15 |
| /29	| 255.255.255.248	| 8	| 0.0.0.7 |
| /30	| 255.255.255.252	| 4	| 0.0.0.3 |
| /31	| 255.255.255.254	| 2	| 0.0.0.1 |
| /32	| 255.255.255.255	| 1	| 0.0.0.0 |

Now here is that tool I mentioned, it is extremely simple, but so powerful as you’ll see in a sec. I would recommend familiarizing yourself with this tool so that you can see a visual representation of how subnetting works for splitting up a network into smaller sub-networks.

[DavidC Subnet Tool](https://www.davidc.net/sites/default/subnets/subnets.html)

## Point-to-Point Links

For most networks, at least two addresses are reserved: the gateway and the broadcast. Now there are cases where you can get away with only having two hosts, such as a /31. The main case for that is point-to-point links, such as is common for uplinks/downlinks between routers and switches. 

*Hint: you’ll want to remember that. It’ll come in handy in a few labs down the road.*

A /31 and /32 were added as part of RFC 3021. Specifically, to reduce the number of needed addresses for point-to-point links. Now, word of caution. If you are not setting up a point-to-point link, I would highly advise against using a /31. In cases where you are not doing so, I would recommend a /30 or a /29 depending on your use case.

## Localhost

Last thing, IP address is very specific for localhost. It is also defined under RFC 1918 as follows:
127.0.0.1 – 127.255.255.255. In most cases 127.0.0.1 is the one that you will be concerned with. This address space is specifically reserved for loopback addresses on a given device.

## Subnetting Practice

Note: The following questions are all for a 10.0.0.0/16 network
-	Say you needed a /17 and 4x /20s. What does that look like (what are the different IP ranges for those subnets)?

-	Now say you need to split that even further to 8x /20s. What does that look like?

## Write-up Questions
-	What does RFC stand for?

-	What does IANA stand for? What is its purpose?

-	What does CIDR stand for?

-	To which Classes does CIDR apply?

- What class level is your home network?

-	What class level is BYU’s public network?

-	How many hosts are in a /25 network?

-	How many hosts are in a /30 network?

-	Can you think of a good case for using a /31 network? 

## Resources

-	https://www.lifewire.com/what-is-a-public-ip-address-2625974
-	https://www.omnisecu.com/tcpip/what-are-private-ip-addresses.php
-	https://www.ionos.com/help/server-cloud-infrastructure/private-network/private-ip-address-ranges/
-	https://en.wikipedia.org/wiki/Private_network
-	https://en.wikipedia.org/wiki/Network_address_translation
-	https://networklessons.com/subnetting/subnetting-in-binary
-	https://www.davidc.net/sites/default/subnets/subnets.html
-	https://www.calculator.net/ip-subnet-calculator.html
-	https://youtu.be/_IOZ8_cPgu8
-	https://packetlife.net/blog/2008/jun/18/using-31-bit-subnets-on-point-point-links/

## Credit
Image credits to TechTarget.com and Tripod.com and video credits to PowerCert Animation

Lab credits to Nathan Moser as the sole author and editor. Additional credit to Bryan Wood for the structure and concepts of the lab.
