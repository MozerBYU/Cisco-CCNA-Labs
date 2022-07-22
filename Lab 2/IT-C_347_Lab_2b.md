## IT-C 347 Lab 2b
### *Practical Lab - Ethernet Patch Panels*
## Introduction

Now that you are familiar with creating an ethernet patch cable, we’ll dive into connecting those cables (at least end of it) to an ethernet patch panel or an ethernet keystone jack. This part is more on the side of networking, as this is where you create the actual terminations for each end of the ethernet line, but it is still a useful skill regardless of the route you take in IT/Cybersecurity.

## Importance of Patch Panels

To explain the usefulness of this skill let me give you a scenario. You’re a new IT admin, and you have the job of setting up a new buildings network. After many long hours of making all of your ethernet runs from individual jacks in each office to an IT closet of sorts. You try to decide how to terminate all those ends in the closet. Do you have all those runs terminate into RJ45 jacks that you plug into your switch? Or do have them terminate to jacks within the closet, that you’ll then connect to the switch?

One certainly seems like more work but is better for general practice and ease of use as needs change (network wise) throughout the company. 

It is best practice to have all ethernet runs terminate to a jack (on the client side) and to a patch panel (on the admin side) so that you can connect new ethernet lines as you deem appropriate according to your needs. Plus, it looks much cleaner. Let me show you what I mean.

## A Nightmare vs A Crisp Setup

This is the first method, where all lines go straight to the switches.

![An IT Nightmare](/assets/images/lab2b/it-living-nightmare.jpg "An IT Nightmare")
 
Does not the above image fill you with fear and pure disgust? It should. Can you imagine trying to troubleshoot a run that has gone bad? Or even trying to find a switch that has died and needs replacing (have fun keeping track of each run and what port they were plugged into.

Now behold why patch panels reign supreme.

![Crisp Cable Management](/assets/images/lab2b/crisp-cable-management.jpeg "Crisp Cable Management")

See why this is so much better, from both a fire-hazard free standpoint, and from an IT administration standpoint? It’s just so crisp and clean. This is the ideal you should strive for in your cable management in networking.

Here’s another from a data center. Isn’t it just so aesthetically pleasing?

![Gorgeous Data Center Cable Management](/assets/images/lab2b/its-gorgeous.jpg "Gorgeous Data Center Cable Management")

In networking, zip ties and velcro are your friend. Use them to keep everything a nice, neat and clean. The patch panel serves as an easy termination point for the ethernet runs, so that you can connect, disconnect runs to your switches with ease. Plus, if anyone replaces you in your position, they won’t hate your guts and burn everything and start all over.

Now you can still use patch panels and create an impending IT disaster. See the following:

![An attempt, but still a failure](/assets/images/lab2b/an-attempt.webp "An attempt, but still a failure")

Don’t do that. One, your career in networking will be very short. And two, no one will like you, nor promote you, and rightfully so, you psychopath.

## Connecting to a Patch Panel

Like with creating an ethernet patch cable, we need some things:
-	Punch down tool
-	Patch panel
-	Ethernet patch cable

Below is a picture of the back of a standard Cat 5e patch panel:

![Patch Panel Backside](/assets/images/lab2b/patch-panel-backside.jpg "Patch Panel Backside")
 
More or less, find the color of the wire that matches the color on the little picture, then put the wire in the slot and use the punch down tool to secure the wire. Like with the prior lab, you’ll know you did wrong if you test it with speed test and you only get 100 Mbps, or not connection at all. Which means, yep, you get to redo it. 

Like with the prior lab, here’s a YouTube video demonstrating how to do this:
https://www.youtube.com/watch?v=TgvmM6R8rQc

## Resources
-	https://fibertronics.com/how-to-punch-down-a-cat-cable-into-a-patch-panel
-	https://www.spacejam.com/1996/

# Credit

Image credit to DotCom-Monitor.com, Medium.com and LinkedIn.com. 
