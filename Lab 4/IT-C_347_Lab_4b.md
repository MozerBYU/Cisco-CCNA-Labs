# IT-C 347 Lab 4b
### *Practical Lab - Cisco Switch Password Reset and Firmware Upgrade*
## Introduction

*Note: This is a **GROUP ASSIGNMENT**. Please work together on this*

Something that you are most certainly going to come across in your days as an IT administrator, technician, network engineer, etc, is discovering that the previous employee in X position forgot to leave you with the password to a device. Hopefully, in the Operating Systems class they will cover how to change a server password that you don’t know, as we won’t cover that here. However, we will cover the basic general concept for switches/routers. Now, we are going to specifically focus on Cisco hardware, but the general concept applies to most switches/routers.

## Cisco Hardware

The switch we’ll be dealing with will be the Cisco Catalyst 3850 48 POE+. 

![Cisco 3850 Switch](/assets/images/lab4b/cisco-3850-switch.png)
 
Now, some things to be aware of. Cisco hardware runs on their own proprietary OS called iOS. Surprising they’re not in a legal battle with Apple over that, but that’s beside the point. Learning how to program and troubleshoot Cisco hardware from the terminal is a difficult learning curve. For this lab I will be showing you the EXACT commands that you need to run. 

You’re probably wondering how effective that is in helping you learn. And you’re correct, I am guiding you through the steep learning curve that is learning Cisco iOS. And here’s why, come these next few labs you are all on your own, obviously I will still help. But in these next few labs you will have to google how to do everything. Much like the labs from IT-C 210, you will be more or less on your own. 

At least for this lab, rather than baptizing all of you in fire to start with, I decided to guide you part way across the bridge above the lava, and then push you in. You’re welcome!

But knowing even the most basic commands like “enable” and “configure terminal” (hence known as “conf t”) are super helpful. And will give you a stepping stone of sorts for next few labs. As without either of these commands you can do absolutely nothing on Cisco iOS. 

## Tools

However, before we dive into the actual commands, we need to go over some standard tools that you’ll need to connect to these switches (and most networking gear for that matter). Most networking gear or even some old legacy servers and desktops come with serial ports or console ports, that are used for console access. 

Those ports will look like the following:

![Serial Port](/assets/images/lab4b/serial-port.jpg)

![RJ45 Port](/assets/images/lab4b/cisco-switch-rj45-port.jpg)
 
In order to connect to these ports you’ll need one or the other of the following cables
-	USB-to-Serial (female) cable
-	USB-to-RJ45 cable

Those will look like the following:

![USB-to-Serial](/assets/images/lab4b/usb-to-serial.jpg)

![USB-to-RJ45](/assets/images/lab4b/usb-to-rj45.jpg)
                  
## Setup

To begin, connect either the serial or RJ45 cable to the switch and the USB side to your laptop. Next, you’ll need a program called PuTTY, or the equivalent. Now the next part depends on what machine you are using. If it is a Windows you’ll need to identify what serial port your cable is connected to on your computer (this is easily found within Device Manager). 

Some important things to know about serial connections (note: this will be covered more in the Digital Communications class). They are known as serial because the device ‘serializes’ the data, as in it sends all 8 bits of data in one byte chunks. For each serial connection there is a specified bit rate that each device must be set to, in order for the data to be sent and received correctly.

Next, you’ll want to configure your PuTTY settings as follows:
-	Speed: 9600 (or whatever the device requires, in our case it is 9600)
-	Connection Type: Serial
-	Serial Line: the COM port you found in Device Manager

It should look similar to the following:

![Putty Configuration Screen](/assets/images/lab4b/putty-configuration.png)

Lastly, you’ll want to power on the switch, immediately pressing and holding the ‘mode’ button. Hold it down for approximately 12 or so seconds, until the SYST Status LED goes amber. On the console you should now be in the ‘boot loader’, denoted by a prompt similar to the following:

> `Switch:`

![Cisco Mode Button](/assets/images/lab4b/cisco-mode-button.jpg)
 
## iOS Commands

Before we get into the actual commands, you need to know a bit about how Cisco iOS works. 

You have essentially 3 modes that you will switch between on the command-line (you'll notice similaries to the Unix command-line):  
- Unprivileged
- Privileged
- Configuration

To get to the privileged mode, you need to use the “enable” command. This allows you to view settings on the switch/router. Now in order to make changes you need to be in configuration mode, using the command “conf t” (short for ‘configure terminal’).

Another important command is "do" (think of it like using 'sudo').

## Password Recovery Commands

Now for the tough part, lol. All you need to do is copy the following commands in order:

*// Tell the switch to ignore the startup config*
<br> `Switch: SWITCH_IGNORE_STARTUP_CFG=1`

*// Tell the switch to enable password recovery*
<br> `Switch: SWITCH_DISABLE_PASSWORD_RECOVERY=0`

*// Soft reboot the switch*
<br> `Switch: boot`

*// Copy the running config into flash memory*
<br> `Switch# copy start run`
 
*// Then hit ENTER to copy the running-config*

*// Enter a config terminal*
<br> `Switch# conf t`

*// From here you can set a password*
<br> `Switch (config)# enable secret <password>`

*// Tell the switch to run the startup config*
<br> `Switch# SWITCH_IGNORE_STARTUP_CFG=0`

*// Finally, tell the switch to disable password recovery*
<br> `Switch (config)# system disable password recovery switch all`

*// Copy the running config into flash memory*
<br> `Switch# copy start run`
 
*// Then hit ENTER to copy the running-config*

*// Then reboot the switch*
<br> `Switch# boot`

## Firmware Upgrade Commands

Before you begin this part, you will need to download the firmware upgrade .bin file from LearninSuite under 'Content', 'Labs' and then 'Lab Software', titled "cisco_3850_new.bin".

*// Find the switch firmware version number*
<br> `Switch# show version`
<br> `-	16.09.04`

*// Copy the config file from Cisco’s website to flash memory*
<br> `Switch# copy usbflash0:<file_name> flash:`

*// Enter a config terminal*
<br> `Switch# conf t`

*// Then apply the firmware update*
<br> `Switch# (config) boot syst switch all flash:<firmware_update_file_name.bin>`

*// Exit the config terminal*
<br> `Switch# (config) exit`

*// Then apply the new configur*
<br> `Switch# copy start run`

*// Then hit ENTER to copy the running-config*

*// Tell the switch to run the startup config*
<br> `Switch# SWITCH_IGNORE_STARTUP_CFG=0`

*// Verify new boot variable is set to new config file*
<br> `Switch# show boot`

*// Then reboot the switch*
<br> `Switch# boot`

*// Finally check the version to make sure it updated correctly*
<br> `Switch# show version`
<br> `-	16.12.05`

## Write-up Questions
 
As part of you write up include a screenshot of the terminal once you have reboot the switch demonstrating that you have reset the password (by disabling it).
-	What are the three modes in Cisco iOS?

-	What does ‘configure terminal’ or ‘conf t’ do?

-	What does the command ‘copy start run’ tell the switch to do?

-	How is that command different from ‘write memory’?

-	Why does the bit/baud rate on the switch need to be 9600?

-	How does a serial connection work?

## Pass-off

For pass-off, we just need a screenshot of the PuTTY terminal that you have completed each portion (password reset, and firmware upgrade). You’ll turn these in as part of your write-up submission.

## Resources
-	https://www.netwrix.com/cisco_commands_cheat_sheet.html

## Misc Resources for Troubleshooting the Cisco Switches
- https://community.cisco.com/t5/switching/changeing-flash-from-read-only-to-read-write/td-p/3739978
- https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3850/software/release/3se/system_management/configuration_guide/b_sm_3se_3850_cg/b_sm_3se_3850_cg_chapter_01110.html#task_1021182

## Credit

Image credits to PuTTY, CablesandKits.com, Amazon, Cisco, Wikipedia and Snabay Networking.

Lab credits to Nathan Moser as the sole authors and editor, and Albert Tay for the structure and concepts of the lab.
