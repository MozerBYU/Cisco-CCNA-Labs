# IT-C 347 Lab 4a
### *Practical Lab - Cisco Switch Password Reset*
## Introduction

Something that you are most certainly going to come across in your days as an IT administrator, technician, network engineer, etc, is discovering that the previous employee in X position forgot to leave you with the password to a device. Hopefully, in the Operating Systems class that will cover how to change a server password that you don’t know, as we won’t cover that here. However, we will cover the basic general concept for switches/routers. Now, we are going to specifically focus on Cisco hardware, but the general concept applies to most switches/routers.

## Cisco Hardware

The switch we’ll be dealing with will be the Cisco Catalyst 3850 48 POE+. 

![Cisco 3850 Switch](/assets/images/lab4a/cisco-3850-switch.png "Cisco 3850 Switch")
 
Now, some things to be aware of. Cisco hardware runs on their own proprietary OS called iOS. Surprising they’re not in a legal battle with Apple over that, but that’s beside the point. Learning how to program and troubleshoot Cisco hardware from the terminal is a difficult learning curve. For this lab and the next (5b) I will be showing you the EXACT commands that you need to run. 

You’re probably wondering how effective that is in helping you learn. And you’re correct, I am guiding you through the steep learning curve that is learning Cisco iOS. And here’s why, come Lab 6b you are all on your own. In that lab you will have to google how to do everything. Much like the labs from IT-C 210, you will be more or less on your own. Rather than baptizing all of you in fire to start with, I decided to guide you part way across the bridge above the lava, and then push you in, in Lab 6b. You’re welcome!

But knowing even the most basic commands like “enable” and “configure terminal” (hence known as “conf t”) are super helpful. And will give you a stepping stone of sorts for Lab 6b. As without either of these commands you can do absolutely nothing on Cisco iOS. 

## Tools

However, before we dive into the actual commands, we need to go over some standard tools that you’ll need to connect to these switches (as most networking gear for that matter). Most networking gear or even some old legacy servers and desktops come with serial ports or console ports, that are used for console access. 

Those ports will look like the following:

![Serial Port](/assets/images/lab4a/serial-port.jpg "Serial Port")

![RJ45 Port](/assets/images/lab4a/rj45-console-port.png "RJ45 Port")
 
In order to connect to these ports you’ll need one or the other of the following cables
-	USB-to-Serial (female) cable
-	USB-to-RJ45 cable

Those will look like the following:

![USB-to-Serial](/assets/images/lab4a/usb-to-serial.jpg "USB-to-Serial")

![USB-to-RJ45](/assets/images/lab4a/usb-to-rj45.jpg "USB-to-RJ45")
                  
## Setup

To begin, connect either the serial or RJ45 cable to the switch and the USB side to your laptop. Next, you’ll need a program called PuTTY, or the equivalent. Now the next part depends on what machine you are using. If it is a Windows you’ll need to identify what serial port your cable is connected to on your computer (this is easily found within Device Manager). 

Some important things to know about serial connections (note: this will be covered more in the Digital Communications class). They are known as serial because the device ‘serializes’ the data, as in it sends all 8 bits of data in one byte chunks. For each serial connection there is a specified bit rate that each device must be set to, in order for the data to be sent and received correctly.

Next, you’ll want to configure your PuTTY settings as follows:
-	Speed: 9600 (or whatever the device requires, in our case it is 9600)
-	Connection Type: Serial
-	Serial Line: the COM port you found in Device Manager

It should look similar to the following:

![Putty Configuration Screen](/assets/images/lab4a/putty-configuration.png "Putty Configuration Screen")
 
## iOS Commands

Now for the tough part, lol. Before we get into the actual commands, you need to know a bit about how Cisco iOS works. 

You have essential 3 modes: 
- Unprivileged
- Privileged
- Configuration

To get to the privileged mode, you need to use the “enable” command (think of it like using sudo). This allows you to view settings on the switch/router. Now in order to make changes you need to be in configuration mode, using the command “conf t” (short for ‘configure terminal’).

## Resources
-	https://www.netwrix.com/cisco_commands_cheat_sheet.html

## Credit

Image credits to some people.
