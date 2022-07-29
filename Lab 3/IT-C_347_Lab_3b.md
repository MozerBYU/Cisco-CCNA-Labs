# IT-C 347 Lab 3b
### *Practical Lab - Subnetting*
## Introduction

If all went well in Lab 1, you should have the GNS3 software and VM setup correctly. You’ll know if when you open the GNS3 software, it’ll be immediately followed by the VMWare Workstation software opening to load the GNS3 VM.

To start off this lab, let me give you an overview of what we’re trying to achieve throughout all the labs at the end of Lab 6:

![Completed Lab 6](/assets/images/lab3b/completed-lab.png "Completed Lab 6")
 
However, like I mentioned in Lab 1, we will be doing this in chunks so that it is consistent with what you’re learning in the conceptual labs and in class, and so that you don’t get overwhelmed. 
For now, we’re going to focus on setting up our lab so that it looks like the following:

![Starter Lab 3](/assets/images/lab3b/starter-lab.png "Starter Lab 3")
 
Now you are welcome to set your lab however you want. What we’re looking for are 4 different VLANs, you can number these however you want as long as you don’t use VLAN 1. One stipulation though, is that one of those VLANs needs to be completely unroutable (no other VLANs can talk to it, and it can’t talk to any other VLANs. However, the hosts within that VLAN can talk to each other). You can determine how many switches you want, but the minimum is 4. At the end there should be a minimum of two distribution routers and two core routers. 

*Note: If you want to add more hosts, switches, distribution routers and core routers, be my guest. But complexity is not the goal here. We’re focusing on learning the concepts and putting them into practice.*  

## Setup Hosts

First, you’ll want to setup all of your hosts. If you don’t have the ubuntu docker container, go to “Preferences” then “Docker Containers” and then select the option to add a new one. You can use whatever docker image you want, I simply grabbed the official ubuntu image.

Next, you’ll want to setup each of those hosts on their subnets. My advice, figure out what your subnets will be first, before you do this. You can do that with an excel spreadsheet, or a text file. Whatever you choose, you will submit this file as part of your lab pass-off. But please make it look somewhat decent.

This is good practice for creating documentation in the IT industry, which is an ABSOLUTE must, as life is pure pain when you get to a job that has either a) outdated documentation, b) fragmented documentation, or c) the worst of them all, no documentation at all.

To help you in figuring this out, we’ll work on the first VLAN + subnet together. Say we have our two hosts on VLAN 10 for example, and we wanted to use 192.168.x.x/24 for our host networks, then we could make our subnet 192.168.10.x/24 for simplicities sake.

Whatever you choose, choose to be consistent. Don’t have VLAN 10, 20 and 30 with respective subnets of:

-	192.168.10.x/24
-	192.168.20.x/24
-	192.168.30.x/24

And then have VLAN 40 on 192.168.80.x/24. Yes, it will still work, but that’s just annoying. Think of what you would want in industry to see when you get to a new job. You want consistency among the reasons why you choose a subnet to be associated with a particular VLAN. Don’t make your life, or the life of the poor IT guy/gal after you misery. Be consistent, and make decisions that make sense, please.

*Note: You don’t have to put a text box under each host of what the IP address is, but it is highly recommended that at least put what the subnets are for ease of working on the lab down the road.* 

Additionally, you can have the host IP addresses whatever the heck you want in the given network you choose. I recommend using /24 subnets as that will make you life easier for the subnet mask part. I also recommend using IP addresses that make sense. If you recall, DHCP assigns IP addresses with the next available address. Going back to our above example, you could have those two host IP addresses like the following:

-	Host 1: 192.168.10.2
-	Host 2: 192.168.10.3

## Pass-off

Now for pass-off I’m only looking for a few things:

-	1) you have put each of the hosts into 4 separate VLANs
-	2) one of those VLANs you have designated as the unroutable one
-	3) you have a file of some sort that has all the subnets you have chosen
-	4) each host has been assigned an IP address consistent with the given subnet and CIDR that you have chosen

## Credit

All image credit goes to myself.
