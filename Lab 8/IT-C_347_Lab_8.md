# IT-C 347 Lab 8
### *Conceptual/Practical – Network Troubleshooting*
## Introduction

At the completion of Lab 6, you are now ready to put your networking skills to the test and to learn how to do network troubleshooting. This lab is to be done in groups of 3, emulating working with a Networking Team to troubleshoot and remediate a mock networking environment that mirrors 

Your team’s task is to learn the Network Troubleshooting process, via 3 walkthrough-like sub-labs. Then to utilize those skills and demonstrate that you can troubleshoot a network.

The point break-down is as follows

| Lab	| Layer(s)	| Points |
| :------: | :------: | :------: |
| Lab_8_L1	| 1	| 20 |
| Lab_8_L2	| 2	| 20 |
| Lab_8_L3	| 3	| 20 |
| Lab_8_Full	| All (1 - 3)	| 40 |
| Total Points | - |	100 |

## Conceptual Methodology

The following is a thought process I have adopted when doing networking troubleshooting, you can change this if you wish, but it gives you a baseline to build off of. 

When doing network troubleshooting you will go through various layers of the OSI model. But you want to be efficient and not waste time on things, when you can catch an easy problem and fix it without much trouble. 

In general practice I would start at either Layer 3, or Layer 7, and or both. By Layer 3, I mean testing and verifying what the device can talk to. By Layer 7, I mean is there a stupid setting on the OS that you have disabled that is causing you grief. After you have gone to either Layer 3, I would then go to Layer 1 and work my way back up. I would also go from Layer 7 and work my way down. Granted I would give priority to checking Layers 1-3, 7. Reason being, troubleshooting Layers 4, 5 and 6 sucks. This is where TCP/UDP, Segments, TLS, Sessions and dealing with Application/OS Code resides, and boy is it a pain in the neck to deal with, not to mention time-consuming.

### *Quick Sum Up*

Start your troubleshooting with Layer 3, then go to Layer 1 and make your way back up to Layer 3

## Sub-Labs

### *Part 1 – Layer 1 Troubleshooting (20 pts)*

*Note: Use the Lab_8_L1 Lab file for this section*

Layer 1 is where the physical electricity and the 1s and 0s are transmitted and received (denoted by TX/RX and usually blinking orange or green lights on a physical network device). 

Layer 1 in GNS3 includes ports and connections between ports. Some things to check when searching for/addressing Layer 1 issues:
-	Is the device running?
-	Is the cable physically plugged in where should be?
-	Is the port active? (aka not shutdown)
-	Is the cable transmitting/receiving correctly? (including expected speeds)

### *Part 2 – Layer 2 Troubleshooting (20 pts)*

*Note: Use the IT-C_347_Lab_8_L2 Lab file for this section*

Layer 2 is where switches and MAC address operate. To some degree there is also where VLANs operate (within their own VLANs/Subnets). 

Layer 2 in GNS3 includes whether mode a port is in, what VLAN a specific port is assigned, VLAN trunk links, and VLAN databases on switches and distribution routers. Some things to check when searching for/addressing Layer 2 issues:
-	Is the port in its correct access/trunk mode?
-	Is the port in its correct VLAN?
-	Are all necessary VLANs in the VLAN DB?
-	Do any of the hosts have MAC address conflicts?

### *Part 3 – Layer 3 Troubleshooting (20 pts)*

*Note: Use the IT-C_347_Lab_8_L3 Lab file for this section*

Layer 3 is where routers and IP addressing operates. It is also where the VLANs/Subnets fully operate.

Layer 3 in GNS3 includes IPs, Gateways, VLAN SVIs, routing tables, static routes, OSPF, need I continue? Therefore, some things to check when searching for/addressing Layer 3 issues:
-	Is the devices networking configured correctly? (IPs, subnet mask, gateway address)
-	Are the gateways (SVI or otherwise) configured correctly? And are they running and reachable?
-	Are there any routing issues in the routing table?
   -	Static routes misconfigured
   -	OSPF misconfigured
-	Are there any other extraneous issues with routing?

## The Comprehensive Lab of Doom (40 pts)

*Note: Use the Lab_8_Comprehensive Lab file for this section*

Now that you’ve had a fairly good walkthrough of what to look for on the various Layers between 1-3, and have gotten some practice with the pre-labs, it is time to challenge you and put your skills to the test.

You will be given a pre-built lab, very similar to your completed Lab 6b. You and your team’s job are to troubleshoot the network and get it back in working condition. You will need to verify this, so make sure everything is working as expected, and I mean everything, because I will check everything.

I call it the Lab of Doom on purpose, as this is meant to challenge you. It is supposed to be difficult. It will require you to do some googling and to work with your team to figure it out. As such, don’t procrastinate and push it off, or you will fail. 

<ins>**You are restricted from discussing and getting aid from other groups. You can ask TAs/Professors for general methodology questions related to how Layers 1 – 3 work.**</ins>

Good luck, and may the odds ever be in your favor!
 

## Pass-off
-	1) You have completed Lab_8_L1
-	2) You have completed Lab_8_L2
-	3) You have completed Lab_8_L3
-	4) You have fixed the broken Lab_8_Comprehensive
-	5) You have a summary of what you had to fix for the Comprehensive Lab (this part is an individually submitted assignment)

## Lab Credits

All Lab credits to Nathan Moser (myself).
