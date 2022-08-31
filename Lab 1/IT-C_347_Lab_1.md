# IT-C 347 Lab 1
### *Practical Lab - Software Setup*
## Introduction

We are going to have a lot of fun throughout the semester! We’re going to use the semi-wonderful program called GNS3 (you'll understand later why I say that). It is a very powerful and capable network virtualization program. With it you will be building one master lab over the course of the whole semester, divided in 6 sections. In this lab you will be dealing with lots of networking areas: IP Addressing, Subnetting, VLANs, Switches, Routers, and Packet Capture.

Optionally, we will also have a lab to prepare you for the Advanced Networking class focusing on some advanced routing technologies.

## Cisco Academy

Cisco Academy is a wonderful resource for anyone who wants to grow, deepen or sharpen their networking skills, as Cisco is very dominate in the networking field. In this class we will be focusing a lot on Cisco and Cisco iOS in relation to setting up switches and routers.

To begin, go to the following and create your account:

[Cisco Academy Website](https://www.netacad.com/)

You are welcome to work on any of these labs to further your skills in addition to what we do in this class. Trust me, they will prove a very valuable resource throughout your career, regardless of the field.

There is also a wonderful resource called GNS3 Vault that also has labs that you can work on if you wish.

[GNS3 Vault Website](https://gns3vault.com/)

## GNS3 Install

Now for the fun part, installing GNS3. This comes in 3 parts: installing GNS3, installing VMWare Workstation Pro (or Virtual Box if you really want to hate your life), and importing the GNS3 VM. To get the GNS3 software head to the following website, make an account and then download the software:

[GNS3 Website](https://www.gns3.com/)

Now you can download the GNS3 VM file now if you wish, or it will be downloaded later during the GNS3 install. If you do, make sure you get the one specific to VMWare Workstation Pro. 

*Note: You are welcome to use whatever hypervisor of VM software of your choosing. But for this class we are specifically supporting VMWare Workstation Pro as the VM software of choice.*

For ease of installation and simplicity, we are going to have GNS3 download the VM for us. We'll skip right to installing GNS3. During which you will be presented with a few options. Most of the windows it walks you through are nothing particularly special minus a few:

![GNS3 Components Screen](/assets/images/lab1/gns3-components.png "GNS3 Components Screen")

Make sure to select both ‘GNS3 Desktop’ and ‘GNS3 VM’. If you don’t, you’ll have some fun problems, and you will have to reinstall GNS3. You have been warned.

Next, you’ll want to make sure that the VM type is set to “VMWare Workstation Pro” or to whatever you are using.

*Note: If for whatever reason, you choose to use VirtualBox, you have both my pity and my condolences. This is your last chance to redeem yourself. Any future problems you have from here on out are you own fault.*

![GNS3 VM Type Screen](/assets/images/lab1/gns3-vm-type.png "GNS3 VM Type Screen")

After that screen you should be done. It will take a while to complete the install (roughly 15 - 30 mins, depending on your internet connection and computer).

*Note: Something that is **very important**. The version of GNS3 you have and the version of the GNS3 VM **MUST MATCH**. If they don't GNS3 won't work. Later on, we'll show you how to turn off automatic updates for GNS3.*

## VMWare Workstation Pro Install

VMWare Workstation is an extremely powerful software with great features. BYU has been gracious enough to give us a license as students so that we don’t have to purchase it (hint it’s expensive). This info is all found at [BYU Software Website](https://software.byu.edu/workstation). You can download VMWare Workstation from the following website:

[VMWare Workstation Website](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)

Here is the license key that you will need:
> 450CL-NG19Q-28DJ2-0K3HP-8026H

## GNS3 VM Import

Once that is all installed, you'll be brought to the following screen:

![VMWare Workstation Main Screen](/assets/images/lab1/vmware-main.png "VMWare Workstation Main Screen")

From which you'll select "Open a Virtual Machine", then browse until you find the file that was downloaded by GNS3 (GNS3.VM.VMware.Workstation.2.2.33.1.zip). You'll want to extract that zip, as within it is the GNS3.ova file. It will take a few minutes for VMWare to import the VM. 

From here you'll select "Open a Virtual Machine", then browse until you find the GNS3.ova file that has the VM. It will take a few minutes for VMWare to import the VM.

*Note: Make sure to title the VM: “GNS3 VM”, as this is what GNS3 is looking for when it tries to connect to the VM.*

If everything is working correctly you should see a screen within VMWare Workstation that is similar to the following:

![VMWare Workstation GNS3 VM Screen](/assets/images/lab1/gns3-vm-working.png "VMWare Workstation GNS3 VM Screen")

## Start-up GNS3

Now open GNS3 for the first time, and we'll make sure that everything gets connected properly with the GNS3 VM we just setup.

You’ll be welcomed with a window asking you to create your first project. If you wish you can make a new project for each lab (copying the previous lab), or you can build all off of the same lab. 

![GNS3 New Project Screen](/assets/images/lab1/gns3-new-project.png "GNS3 New Project Screen")

Off to the right-pane is where you can see system stats on your GNS3 VM. If it is green, then you are good to go. If it is red, you’ll need to go into the ‘Preferences’ pane under ‘Edit’ to fix that.

That will bring up a window like the following:

![GNS3 Preferences Screen](/assets/images/lab1/gns3-preferences.png "GNS3 Preferences Screen")

There are many options that you are welcome to adjust. We’re specifically here to adjust the following:
-	Server: has the settings for connecting to a local or remote GNS3 VM instance
-	GNS3 VM: this has all the settings for connection to your GNS3 VM itself
-	Packet Capture: this has all the settings for connecting to WireShark
-	Dynamips: this is where we will import our router template that we will use for our Cisco switches and routers
-	Docker containers: this is where we will import a Ubuntu 20.04/22.04 docker instance for our hosts

## GNS3 VM Settings

Now that GNS3 and the VM are ready to go, we need to update the resources allocated to our VM so it has better performance. You can adjust these to your liking and to the extent your system can handle. 

These are the minimum recommended settings for the labs:
-	vCPU Cores: 4
-	RAM: 1 GB

If you’re system can handle it, these are the recommended settings for the labs:
-	vCPU Cores: 4
-	RAM: 4 GB

Note: The settings changed within GNS3 will automatically apply to the VM. You do not need to change these settings within VMWare Workstation.

Last thing, you’ll want to go in and change GNS3 to not auto-update. Because if it does, either you’ll have to reinstall GNS3 or reimport the latest version of the GNS3 VM, both of which will be total headaches.

![No Auto-Update GNS3](/assets/images/lab1/gns3-no-update.png "No Auto-Update GNS3")

## Additional Software

Like was mentioned earlier we’ll need to import our Cisco switch/router file and a docker container for Ubuntu 20.04/22.04.

The file for the Cisco switch/router can be found on LearningSuite under ‘Content’, ‘Labs’, then under 'Lab Software', tiled "cisco_3275_router.bin".

You’ll have to manually get the Ubuntu docker container file (we’ll go over this in class if you get stuck).

## Resources

- https://www.netacad.com/
- https://gns3vault.com/
-	https://www.gns3.com/

## Credit

Image credits to VMWare and GNS3.

Lab credits to Nathan Moser as the sole author and editor. Additional credit to Bryan Wood for the structure and concepts of the lab.


