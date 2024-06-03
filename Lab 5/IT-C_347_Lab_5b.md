# IT-C 347 Lab 5b
### *Practical Lab – VLANs*
## Introduction

Now that you have learned way more than you’ll ever need to know about VLANs, we’re ready for the next step in our GNS3 lab, setting up VLANs with Distribution Routers.

For this next section, we’re going to focus on setting up our lab so that it looks like the following:

![GNS3 Lab 5 Final](/assets/images/gns3/Lab-5.png)

For this lab, you need to set up 2 Distribution Routers, connect them to each of your 4 switches, and then set up the VLAN SVIs on the routers.  
## Conceptual Methodology

To help explain how to do this lab, I’m going to go over the lab from a high-level conceptual standpoint.

If you recall, these labs build on each other. As such, you shouldn’t be changing anything from the last two labs. Instead, you are adding things to what is already there.

Basically, what we’re doing is setting our switches into port-based VLANs, creating trunk links to our distribution routers, creating VLANs on each of our switches/distribution routers and adding them to the VLAN database, and then creating VLAN SVIs on our distribution routers.

In this setup our switches are strictly Layer 2, all they handle is traffic inter-subnet/inter-VLAN, assigning each host as to what VLAN they are in. And then our distribution routers are Layer 3 switches. As such they are going to handle all the routing between our subnets and VLANs. It is also where all our gateways will reside.

## Lab Setup 
### *Setup Distribution Routers*

If you recall from Lab 4c, we setup an EtherSwitch template image. We will be using that image for setting up both our Distribution Routers in this lab, and our Core Routers in Lab 6b. If you use the other image that we used for the switches, you are going to run into a lot of issues. 

### *Switch vs Router Modules*

First, let’s briefly review how switch/router modules are setup on a given Switch/Router in GNS3. The following image from GNS3’s forums is very helpful in this understanding:

![GNS3 Switch vs Router Modules](/assets/images/lab5b/gns3-modules.png)
 
The modules are structured as follows:
-	f0/# -> these are routing interfaces
-	f1/# -> these are switchport interfaces

In the previous lab and this lab, you only want to use the switchport interfaces, if you don’t things will get interesting. As these operate on Layer 2. In the next lab, Lab 6b, we will start using the routing interfaces.

### *Switches*
In the last lab, you set up each port going to each host in access mode. First, thing we’re going to do is go back to each interface and modify the configuration such that each port is also in its appropriate VLAN. This is done via the following command:
> `switchport access vlan <vlan-id>`
  
Next, you need to add each VLAN to the VLAN Database on each switch. This can be done by running the following command, respective to the VLAN you are configuring:
>	`vlan <vlan-id>`
  
### *Distribution Routers*
Now on these we need to set our VLAN SVIs, which simply put is creating a VLAN gateway. Each network needs a gateway in order to talk to other networks, this includes VLANs. To create these we’ll following the instructions here:
  
https://www.grandmetric.com/knowledge-base/design_and_configure/how-to-create-svi-interface-cisco/
  
Basically, you need to add each VLAN to the VLAN Database:
> `vlan <vlan-id>`
  
And then you need to create the actual VLAN SVI for each of your VLANs that are routable
> `int vlan <vlan-id>`
> <br>	`ip address <ip_address> <subnet_mask>`
> <br> `no shut`
  
*Note: For your un-routable VLAN you will not create a VLAN SVI*

Next, we need to ensure that routing is enable on our Distribution Routers, and only our Distribution Routers. These changes these from L2 switches to L3 switches:
> `ip routing`
  
### *Trunk Links*
  
Next, we need to create a new interface on both our switches for our trunk links. This can be done by going into the respective interface on each you plan to use and running the following command:
> `switchport mode trunk`
  
Next, we need to specify what VLANs are allowed to traverse that trunk. Now there are two ways to do this, either A) you can explicitly specify which VLANs are allowed (better security), or B) you can allow all VLANs by default (better management and ease of setup).
  
In this lab, we’re not super concerned about security, as it is more about the networking concepts, so if you want to allow all VLANs that is sufficient. 

Either way here are the respective commands:
> Specifying a VLAN list: `switchport trunk allowed vlan add <vlan-id-1>,<vlan-id-2>,<vlan-id-3>`
> <br>	Specifying a VLAN range: `switchport trunk allowed vlan add <vlan-id-1> - <vlan-id-2>`
> <br>	Allowing all VLANs: `switchport trunk allowed vlan all`
  
### *Saving Configs*
  
Do note, the command ‘write memory’ is deprecated. And it has also been observed to not save the configs as intended. As such moving forward the command you will use is ‘copy run start’. Be sure to not use ‘copy start run’, as there is a difference.
>	`copy run start` -> copies the running-config to the startup-config
> <br>	`copy start run` -> copies the startup-config to the running-config
  
## Note about SVIs
  
VLAN SVIs are used by the Cisco routers to designate a gateway for a given VLAN subnet. Put simply, a gateway is a central contact point for each host in a given subnet, that allows them to talk outside of their given subnet. In order for each of your hosts to talk outside of their VLAN, they need a gateway, to tell them how to talk to the other subnets. 
  
Now, don’t get confused. You don’t need a gateway for a host to talk to another host on a given subnet or VLAN. But you do need a gateway to talk to other hosts on other subnets or VLANs. We’ll dive more into why this is, in the next lab on routing. 
  
*Note: Since SVIs make it so that a given subnet can talk to another, for your un-routable VLAN you DO NOT want an SVI. If you do make one it will then be considered routable, as it is able to talk to the other VLANs and they can talk to it*
  
## Troubleshooting
### *General*  
  
General helpful commands for seeing your interfaces, their respective mode, and their respective VLAN if configured:
> `show int status`
> <br>	`show int summary`

Below are helpful commands if you messed up and need to erase the running-config/stored-config:
> `write erase`
> <br> `reload`

Note it will take some time for the switch to reboot and reload everything.
  
### *VLANs aren’t saving in VLAN DB*
  
Some helpful commands with troubleshooting VLANs not being created in the VLAN database:
> `show vlan-switch`
> <br> `show ip int brie`

### *Cisco Extended Vlan not allowed in Current VTP mode*

Basically, by default you are limited to the range of VLAN 1 - 1000. To change this to have the full 1 - 4096 range, run the following command:
> `vtp mode transparent`

## Pass-off
  
Now for pass-off I’m only looking for a few things:
-	1) you have at least 2 distribution routers
-	2) you have at least 4 switches connected to those distribution routers. Preferably, 2 switches to each distribution router
-	3) each host can talk within its subnet, VLAN and can talk outside it’s VLAN relative to the distribution router it is connected to
-	4) for the un-routable VLAN, each host can talk to each other, but cannot talk to the other hosts in other VLANs
  
## Credit
  
All image credit goes to myself, compliments of the GNS3 Software.
  
Lab credits to Nathan Moser as the sole author and editor, and additional credits to Bryan Wood for the structure and content of the labs.
