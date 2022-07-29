# IT-C 347 Lab 3b
### *Practical Lab - Subnetting*
## Introduction

If all went well in Lab 1, you should have the GNS3 software and VM setup correctly. You’ll know if when you open the GNS3 software, it’ll be immediately followed by the VMWare Workstation software opening to load the GNS3 VM.

To start off this lab, let me give you an overview of what we’re trying to achieve throughout all the labs at the end of Lab 6:

![Completed Lab 6](/assets/images/labs/complete-lab.png "Completed Lab 6")
 
However, like I mentioned in Lab 1, we will be doing this in chunks so that it is consistent with what you’re learning in the conceptual labs and in class, and so that you don’t get overwhelmed. 
For now, we’re going to focus on setting up our lab so that it looks like the following:

![Starter Lab 3](/assets/images/labs/lab3b/starter-lab-3.png "Starter Lab 3")
 
Now you are welcome to set your lab however you want. What we’re looking for are 4 different VLANs, you can number these however you want as long as you don’t use VLAN 1. One stipulation though, is that one of those VLANs needs to be completely unroutable (no other VLANs can talk to it, and it can’t talk to any other VLANs. However, the hosts within that VLAN can talk to each other). You can determine how many switches you want, but the minimum is 4. At the end there should be a minimum of two distribution routers and two core routers. 

*Note: If you want to add more hosts, switches, distribution routers and core routers, be my guest. But complexity is not the goal here. We’re focusing on learning the concepts and putting them into practice.*  

## Setup Hosts

Like I mentioned, you can set this up however, you want. If you don’t want to go through the work of putting each host is nice little boxes like I’ve shown above, then you can head to:

https://github.com/MozerBYU/IT-C_347_Labs/assets/files/IT-C-347-Lab-3-Starter.7z

From there you can download a pre-build lab that has all the hosts setup like the picture above.

## Setup Subnets

Next, you’ll want to setup each of those hosts on their subnets. My advice, figure out what your subnets will be first, before you do this.
