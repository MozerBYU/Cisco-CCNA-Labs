# IT-C 347 Lab 4c
### *Practical Lab - Switches*
## Introduction

At this point, you have Lab 3b completed. And should have all your hosts setup in their individual subnets and prepped for their VLANs.

For this next section, we’re going to focus on setting up our lab so that it looks like the following:

![Lab 4 Completed](/assets/images/gns3/Lab-4.png)
 
*Note: We are NOT setting up VLANs yet. That is in the next lab. Rather, we are placing each of our switches and connecting them to the hosts. There should be 4 switches in total. How you choose to connect them doesn’t particularly matter. I put mine as above for ease of visualizing.*

## Import GNS3 Switch Image

First, you need to go to LearningSuite and download the router image. It is under ‘Content’, ‘Lab Software’ title ‘cisco_3725_router.bin’. It’s a bit of a hefty file, so be prepared. We are going to user this router template for both our switches and our routers in the lab. I’ll show you how to setup each exactly so that they work properly. 

*Note: please follow the next set of instructions carefully, or otherwise you could end up switching up the needed modules and unintentionally breaking that section of your lab.*

Once you have the router bin file downloaded somewhere on your computer, you’ll want to head into GNS3 under the ‘Edit’ tab, then ‘Preferences’, ‘Dynamips’ and then the ‘IOS Routers’ section. 

Now, quick note. You will need to run through the following steps twice. Once for the switch and once for the router. We will use the router for both our Distribution routers in Lab 5 and our Core routers in Lab 6.

That screen will have an option to select the ‘New’ tab as show below:

![IOS Router Import](/assets/images/lab4c/import-ios-routers.png)
 
From here you want to select to run the IOS router within your GNS3 VM. You can run it on your local computer, but since we already have the GNS3 VM running everything else, it would be impractical to not use it.
 
![IOS Router Import Settings](/assets/images/lab4c/ios-router-import-settings.PNG) 

Next, we need to import that router image that we downloaded using the ‘Browse’ tab.

![New IOS Router Image](/assets/images/lab4c/new-ios-image.PNG)
 
This is where it gets a bit tricky. For the switch you NEED to select ‘This is an EtherSwitch Router’ as then name it similar to "EtherSwitch", delete the router part as that is confusing. For the routers, you DO NOT want to select 'This is an EtherSwitch Router' as it is not necessary. This will ensure you have the correct icons.

**For the Switch**									             

![EtherSwitch Setup](/assets/images/lab4c/etherswitch-new.PNG)

**For the Router**

![EtherSwitch Router Setup](/assets/images/lab4c/etherswitch-router-new.PNG)
       
After that you’ll have a window to setup how much RAM each switch/router should have. The default is 128 MB which is plenty sufficient in my experience. Plus, you’ll want to keep that number decently low as in the end you’ll have 4 routers and 4 switches running for a total of 2GB, not including the hosts. As such, you don’t want to over-allocate RAM as it is unnecessary, unless of course you have a ton of RAM (16GB +) then, more power to ya.

## Setup Switch Modules

Next, is setting up the switch modules. This is the part that you need to be very careful you follow directions exactly, or your labs won’t work as intended.

For switches your modules should be as follows:
-	Slot 0: GT96100-FE
-	Slot 1: NM-16ESW

Slot 0 is going to be used for communicating up to the Distribution routers (interface(s) f0/#), there should only be 2 of these (f0/0 and f0/1).

Slot 1 is going to be used for communicating down to the hosts (interface(s) f1/#), there should be 16 of these (from f1/0 through f1/15).
 
![EtherSwitch Modules Setup](/assets/images/lab4c/etherswitch-switch-modules.PNG)

## Setup Router Modules

For the routers your modules should be as follows:
-	Slot 0: GT96100-FE
-	Slot 1: NM-1FE-TX
-	Slot 2: NM-1FE-TX

Slot 0 is going to be used for communicating up to the Core routers (interface(s) f0/#), there should only be 2 of these (f0/0 and f0/1).

Slot 1 and Slot 2 are going to be used for communicating down to the Switches (interface f#/0), there are only two of these (f1/0 or f2/0).
 
![EtherSwitch Router Modules](/assets/images/lab4c/etherswitch-router-modules.PNG)

## Modify Memory Settings

After you have setup the switch and router templates, we need to modify the memory settings for each. You can do this by finding the template, going to 'Edit' and then finding the 'Memory Settings' tab. Initially, the setting is 256 KiB of RAM, we’re going to increase that to 64000 KiB of RAM.

You should see a menu similar to the following:
 
![Modify NVRAM Settings](/assets/images/lab4c/increase-nvram.PNG)
 
The option you want to change is the NVRAM to 64000 KiB.

Once that is done, we also want to check the box to ‘Automatically delete NVRAM and disk files’. This helps things run smoother and not over-clutter your computer’s disk space.

## Setup Switches

After you have saved your EtherSwitch and your EtherSwitch router, we are ready for the next section, which is to connect all your hosts to the respective switches, as you have designated. First, begin by setting aside 4 switches, and then work on connecting each to each of the hosts that you want. 

Like was mentioned earlier in a previous lab, you can set this lab up however you want. But there are some restrictions that I will detail in the pass-off section. Aside from these, you can do whatever you want. 

Important note about connecting each host to each switch: When connecting the wiring from a host to the switch you'll want to make sure to use the NM-16ESW module (denoted by f1/#). Don't use the other module (denoted by f0/#) or you will run into some issues (those are used for connections between routers -> trunk links).

Once you have all the switches placed in GNS3 and connected to each of the hosts there are few things you need to do:
-	Set each interface to access mode
- Set each interface to not shut off

Yes, you will need to google how to do this. Good luck!

## Final Note on All GNS3 Devices

One important thing to do on each device (host, switch, router) is set Idle-PC, if you don't it will rack your CPU usage absolutely ridiculously high. To do this, right-click on a given device and find the "Idle PC" option. That will bring up a window that looks like the following: 

![Idle PC Option Menu](/assets/images/lab4c/idle-pc-option.PNG)

It will take your machine a few seconds to calculate the Idle PC Values. You will then have a few options of values you can select. Ideally, you want to choose one with an * next to, as shown in the picture above. If there isn't don't worry about and select whichever one you wish.

# Pass-off

Now for pass-off I’m only looking for a few things:
-	1) you have at least 4 switches (with the correct modules)
-	2) you have at least 2 hosts connected to each switch
-	3) each host can talk within its subnet relative to the switch that it is connected to

## Credit

All image credit goes to myself, compliments of the GNS3 Software.

Lab credit to Nathan Moser as the sole author and editor, additional credit to Bryan Wood for the structure and concepts of the labs.
