# IT-C 347 Lab 3b
### *Practical Lab - Subnetting*
## Introduction

If all went well in Lab 1, you should have the GNS3 software and VM setup correctly. You’ll know if when you open the GNS3 software, it’ll be immediately followed by the VMWare Workstation software opening to load the GNS3 VM.

To start off this lab, let me give you an overview of what we’re trying to achieve throughout all the labs at the end of Lab 6:

![Completed Lab 6](/assets/images/gns3/Lab-6.png)
 
However, like I mentioned in Lab 1, we will be doing this in chunks so that it is consistent with what you’re learning in the conceptual labs and in class, and so that you don’t get overwhelmed. 

For now, we’re going to focus on setting up our lab so that it looks like the following:

![Completed Lab 3](/assets/images/gns3/Lab-3.png)
 
Now you are welcome to set your lab however you want. You can determine how many switches you want, but the minimum is 4. At the end there should be a minimum of two distribution routers and two core routers. 

*Note: If you want to add more hosts, switches, distribution routers and core routers, be my guest. But complexity is not the goal here. We’re focusing on learning the concepts and putting them into practice.*

## Setup Hosts

First, you’ll want to setup all of your hosts. You can use what container for this you want, as long as it has the ability to ‘ping’. For my purposes, I’ll be using the default VPCs image that comes pre-installed with GNS3.

![GNS3 Setup VPCs](/assets/images/lab3b/gns3-interface-vpcs.png)

*Note: Now GNS3 will probably ask you if you want to put that VPC on your local machine or your GNS3 VM. Put it on the VM as that's why we set it up*

Next, you’ll want to setup each of those hosts on their subnets. So for example, you can set a subnet as 10.0.10.0/24, or you could do 192.168.1.0/27. You can make them whatever you want. My advice, figure out what your subnets will be first, noting that will be connecting these with VLANs in Lab 5b. You can do that with an excel spreadsheet, or a text file. Whatever you choose, you will submit this file as part of your lab pass-off. But please make it look somewhat decent.

This is good practice for creating documentation in the IT industry, which is an ABSOLUTE must, as life is pure pain when you get to a job that has either a) outdated documentation, b) fragmented documentation, or c) the worst of them all, no documentation at all.

*Note: You don’t have to put a text box under each host of what the IP address is, but it is highly recommended that at least put what the subnets are for ease of working on the lab down the road.* 

## Setup Host IPs

On each VPC if you right-click and find the 'Edit Config' option, that will bring up a window where you can set the IP of the given host. It should look like the following:

![GNS3 Set VPC IP](/assets/images/lab3b/gns3-set-vpc-ip.PNG)

Now you can have the host IP addresses whatever the heck you want in the given network you choose. I recommend using /24 subnets as that will make you life easier for the subnet mask part, but you do you. You want to make you life extra difficult, I won't stop you. I also recommend using IP addresses that make sense. If you recall, DHCP assigns IP addresses with the next available address. Going back to our above example, you could have those two host IP addresses like the following:

-	Host 1: 192.168.10.2
-	Host 2: 192.168.10.3

The setup of the IP address is as follows: `ip address <ip_address> <subnet_mask>`.

## Note on GNS3 Backups

GNS3 is a great software. However, it is not without error. I can tell you from personal experience, that you’ll want backups of you labs. Both of the whole lab itself (once it is completed), and of the configuration files of the hosts (and later the switches, distribution routers and core routers).
I will show you how to do both.

### *Device Config Backups*

These are done by right-clicking on a given device, going to the ‘Export Config’ option and then exporting them somewhere (I recommend in a folder called ‘config backups’ in your GNS3 project folder).
 
![GNS3 Device Config Backups](/assets/images/lab3b/gns3-interface-device-backup.png)

### *GNS3 Project Backups*

These are done by going to the ‘File’ tab, then going to the ‘Export portable project’ option and saving them somewhere (I recommend NOT saving them in your GNS3 project folder. Preferably, OneDrive/DropBox/iCloud or the equivalent).

Select the following options:
- Include Base Images
- Reset MAC addresses

![GNS3 Project Backups](/assets/images/lab3b/gns3-interface-project-backup.png)

## Pass-off

Now for pass-off I’m only looking for a few things:

- 1) you have a minimum of 8 hosts
-	2) each hosts has been assigned an IP address consistent with the given subnet and CIDR that you have chosen
-	3) you have a file of some sort that has all the hosts, their IPs and the subnets you have chosen

You'll submit that file as well of a screenshot of your lab at this point to LearningSuite.

## Credit

All image credit goes to myself (Nathan)

Lab credits to Nathan Moser as the sole author and editor. Additional credit to Bryan Wood for the structure and concepts of the lab.
