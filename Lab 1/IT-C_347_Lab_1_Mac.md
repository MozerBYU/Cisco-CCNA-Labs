# IT-C 347 Lab 1 – Cisco Academy and GNS3 Setup
### *Practical Lab – Software Setup*
### *MacOSX*
## Introduction

*Note: These instructions are for MacOSX Users*

We are going to have a lot of fun throughout the semester! We’re going to use the semi-wonderful program called GNS3 (you’ll understand later why I say that). It is a very powerful and capable network virtualization program. With it you will be building one master lab over the course of the whole semester, divided in 6 sections. In this lab you will be dealing with lots of networking areas: IP Addressing, Subnetting, VLANs, Switches, Routers, and Packet Capture.

Optionally, we will also have a lab to prepare you for the Advanced Networking class focusing on some advanced routing technologies.

## Cisco Academy

Cisco Academy is a wonderful resource for anyone who wants to grow, deepen or sharpen their networking skills, as Cisco is very dominate in the networking field. In this class we will be focusing a lot on Cisco and Cisco iOS in relation to setting up switches and routers.

To begin, go to the following and create your account:

[Cisco Academy Website](https://www.netacad.com/)

You are welcome to work on any of these labs to further your skills in addition to what we do in this class. Trust me, they will prove a very valuable resource throughout your career, regardless of the field.

There is also a wonderful resource called GNS3 Vault that also has labs that you can work on if you wish.

[GNS3 Vault](https://gns3vault.com/)

## GNS3 Install

Now for the fun part, installing GNS3. This comes in 3 parts: installing GNS3, installing VMWare Fusion Pro (or Virtual Box if you really want to hate your life), and importing the GNS3 VM.  To get the GNS3 software head to the following website, make an account and then download the software:

[GNS3 Website](https://www.gns3.com/)

Now you need to download the GNS3 VM as well, make sure you get the one specific to VMWare Fusion Pro. 

Next, we’ll skip right to installing GNS3. During which you will be presented with a few options. Most of the windows it walks you through are nothing particularly special.

But you should have a wonderful old window like the following when it is done:
 
![GNS3 New Project](/assets/images/lab1/mac/gns3-new-project.png)
 
*Note: You are welcome to use whatever hypervisor of VM software of your choosing. But for this class we are specifically supporting VMWare Fusion Pro as the VM software of choice. If, for whatever reason, you choose to use VirtualBox, you have both my pity and my condolences. This is your last chance to redeem yourself. Any future problems you have from here on out are you own fault*

*Note: Something that is very important. The version of GNS3 you have and the version of the GNS3 VM MUST MATCH. If they don't GNS3 won't work. Later on, we'll show you how to turn off automatic updates for GNS3*

## VMWare Fusion Pro Install

VMWare Fusion Pro is an extremely powerful software with great features. It’s not quite as great as VMWare Workstation Pro, but since you have a Mac it’s the best you got unless you want to pay for Parallels. BYU has been gracious enough to give us a license as students so that we don’t have to purchase it (hint it’s expensive). You can download VMWare Pro from the following website: 

[VMWare Fusion Website](https://www.vmware.com/products/fusion/fusion-evaluation.html)

Here is the license key that you will need:
>	0H2CL-TF31P-K89J2-039KM-1T03H

## GNS3 VM Import

Once that is all installed, you'll be brought a screen that looks like the following:

![VMWare Fusion Main Screen](/assets/images/lab1/mac/vmware-fusion-welcome.png)
 
From which you'll select "Import an existing virtual machine", then browse until you find the file that was downloaded by GNS3 (GNS3.VM.VMware.Workstation.2.2.34.zip). You’ll want to extract that zip, as within it is the GNS3.ovf file you’ll use for the import. It will take a few minutes for VMWare to import the VM. 

*Note: Make sure to title the VM: “GNS3 VM”, as this is what GNS3 is looking for when it tries to connect to the VM*

If everything is working correctly you should see a screen within VMWare Fusion that is similar to the following:

![VMWare Fusion GNS3 VM Screen](/assets/images/lab1/gns3-vm-working-new.png)
 
## Start-up GNS3

Now open GNS3 for the first time, and we'll make sure that everything gets connected properly with the GNS3 VM we just setup.
Now, you will be presented a screen asking you to permit root privileges to uBridge. This is necessary in order for GNS3 to interact properly with the GNS3 VM in VMWare.
 
![GNS3 uBridge Config](/assets/images/lab1/mac/ubridge-config.png)
 
Next, you’ll be welcomed with a window asking you to create your first project. If you wish you can make a new project for each lab (copying the previous lab), or you can build all off of the same lab. 

![GNS3 Welcome Screen](/assets/images/lab1/mac/gns3-new-project.png)
 
Off to the right-pane is where you can see system stats on your GNS3 VM. If it is green, then you are good to go. If it is red, you’ll need to go into the ‘Preferences’ pane under ‘Edit’ to fix that.

That will bring up a window like the following:

![GNS3 Preferences Screen](/assets/images/lab1/mac/gns3-preferences.png)
 
There are many options that you are welcome to adjust. We’re specifically here to adjust the following:

-	Server: has the settings for connecting to a local or remote GNS3 VM instance
-	GNS3 VM: this has all the settings for connection to your GNS3 VM itself
-	Packet Capture: this has all the settings for connecting to WireShark
-	Dynamips: this is where we will import our router template that we will use for our Cisco switches and routers
-	Docker containers: this is where we can import a docker container, if you choose to go that route

## GNS3 VM Settings

Now that GNS3 and the VM are ready to go, we need to update the resources allocated to our VM, so it has better performance. You can adjust these to your liking and to the extent your system can handle. 

These are the minimum recommended settings for the labs:
-	vCPU Cores: 4
-	RAM: 1 GB

If you’re system can handle it, these are the recommended settings for the labs:
-	vCPU Cores: 4
-	RAM: 4 GB

*Note: The settings changed within GNS3 will automatically apply to the VM. You do not need to change these settings within VMWare Fusion*

Last thing, you’ll want to go in and change GNS3 to not auto-update. Because if it does, either you’ll have to reinstall GNS3 or reimport the latest version of the GNS3 VM, both of which will be total headaches.

![No Auto-Updated GNS3](/assets/images/lab1/gns3-no-update.png)
 
## Troubleshooting VM Errors

### *GNS3 VM Network Errors with Local Server*

If you happen to run into the following error: 

“GNS3 VM is not on the same network as the local server”

Don’t worry, you’re not doomed. What you need to do is go to the ‘GNS3’ tab in the top left corner and select the ‘Preferences’ option. That will bring up a window similar to the following:

![GNS3 Preferences Screen](/assets/images/lab1/mac/gns3-preferences.png)
 
From there you want to go to the ‘Server’ tab and find the host binding option and change it so that it is residing on the same network as your GNS3 VM (usually a 192.168.x.x).

![GNS3 Fix Binding Issue](/assets/images/lab1/mac/gns3-fix-binding.png)
 
Now you should be good to power back on your GNS3 VM.

See the following for more info: 
> https://gns3.com/community/featured/gns3-vm-is-not-on-the-same-netwo*

## Pass-off

For pass-off all we're looking for is a screenshot of your GNS3 client that shows two green lights: 

-	1 for your GNS3 client
-	1 for the GNS3 VM.

Once you have that working just submit a screenshot to LearningSuite.

It should look like the following:

![GNS3 Working](/assets/images/lab1/mac/gns3-working.png)
 
## Resources

-	https://www.netacad.com/
-	https://gns3vault.com/
-	https://www.gns3.com/

## Credit

Image credit to VMWare and GNS3.

Lab credits to Nathan Moser as the sole author and editor. Additional credit to Bryan Wood for the structure and concepts of the lab.
