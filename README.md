# IT-C 347 Labs
## Brigham Young University - IT & Cybersecurity Program

These labs are for the IT-C 347 - Networking class, taught in the Fall 2022 Semester.

## Lab Structure

There are 9 labs in total. Labs 2 - 9 are divided in two parts: part A which is conceptual, and part B which is practical. This allows students the ability to learn the concept and have a few write-up questions to test their understanding, and then put that knowledge into practice to solidify it.

### Lab 1: Intro: Setup Cisco Academy and GNS3

In this lab, students setup an account with Cisco Academy and with GNS3. They will then install VMWare Workstation Pro to run the GNS3 VM that we will run our lab in. They will also setup GNS3 and get that connected with the GNS3 VM.

### Lab 2: Networking Cabeling Basics

In this lab, students will get hands-on practice in creating Cat 5e patch cabeling, and performing terminations to network jacks and patch panels. They will also learn about the standards surrounding the various generations of ethernet cabeling from Cat 1 to Cat 7, as well as the respective speeds for each generation.

### Lab 3: IPv4 Addressing and Subnetting

In this lab, students learn about the differences between public IPs and private IPs, how IPv4 classes are setup and the standards surrounding them, as well as how those IP classes relate to classless and classful IP ranges. They will also learn a basic understanding of how gateways and routers help packets get around the internet. Finally, they will learn how subnetting works, how to segregate a larger network into smaller sub-networks using CIDR notation, and how point-to-point links function.

In the practical lab, at this stage the students will setup is the individual hosts on their respective subnets, in preparation for setting them up in VLANs in Lab 5.

The completed lab, to this point, should look like the following:

![Completed Lab 3](/assets/images/gns3/Lab-3.png "Completed Lab 3")

### Lab 4: Switches

In this lab, students will get hands-on practice will a live Cisco switch, a Cataylst 3850 to be exact. In the lab they will learn the basics of Cisco iOS, how to reset a password on a switch, and upgrade the firmware for said device. Additionally, they will learn about the OSI Model, the differences betweem Layer 2 and Layer 3, how switches operate and how switching tables function.

In the practical lab, at this stage the students will then take those hosts from the last lab, and connect them to switches. All hosts should be able to talk within their respective subnets.

The completed lab, to this point, should look like the following:

![Completed Lab 4](/assets/images/gns3/Lab-4.png "Completed Lab 4")
 
### Lab 5: VLANs

In this lab, students will learn more in-depth about the OSI Model, what VLANs are, why they are so useful, how they work, how ethernet frames are setup, and how VLANs relate with subnetting.

In the practical lab, at this stage the students will then put those hosts and switch ports into their respective VLANs. Additional, they we setup 2 distribution routers and connect all switches to said routers. They will then setup the respective SVIs for each VLAN on said router. This is intended as a introduction to routers, and to split of setting up the distribution routers and core routers between two labs. All hosts should be able to talk within their respective subnets and within their respective VLAN (including across subnets). However, host do not need to be able to talk across distribution routers. Hosts in the unroutable VLAN should be able to talk to each other, but not be able to talk to or be talked to by other hosts in other VLANs.

The completed lab, to this point, should look like the following:

![Completed Lab 5](/assets/images/gns3/Lab-5.png "Completed Lab 5")

### Lab 6: Routers

In this lab, students will learn about how routing works, how routing tables function, how to create and setup static routes, and how to implement point-to-point links.

In the practical lab, at this stage the students will then connect the two respective distribution routers to each core router using point-to-point links. Using static routes, they will make it so that hosts can talk from one core router to the other, and vice-versa. All hosts should be able to talk within their respective subnets, vlan, talk across vlans and talk across distribution and core routers. This lab is intended to prepare students for learning about setting up OSPF in the subsequent lab. The full completed lab (combo of Labs 3 - 6) will be tested for completion and then passed-off.

The completed lab should look like the following:

![Completed Lab 6](/assets/images/gns3/Lab-6.png "Completed Lab 6")

### Lab 7: Advanced Networking Technologies (optional)

The purpose of this lab is to introduce students to more advanced routing technologies, like OSPF. As this is more advanced, this lab is optional for students. But is a good preparation for the IT-C 529 - Advanced Networking class if they choose to take it.

In the practical lab, students will go back to their completed lab and will go to the distribution and core routers and remove the static routes they set up. They will then implement OSPF areas and ensure each distribution router and core router can talk across using OSPF.

The complete lab should look like the following: 

![Completed Lab 7](/assets/images/gns3/Lab-7.png "Completed Lab 7")

### Lab 8: Network Troubleshooting

In this lab, students will get hands-on practice with doing network troubleshooting. Students will work in teams for this lab to get them accustomed to working on a IT team in the real-world. They will be given a pre-broken lab, and will need to see if they can figure out what is wrong and get it working again in functionality similar to their completed lab at the end of Lab 6.

### Lab 9: Packet Tracer

In this lab, students will get hands-on practice doing packet tracing using WireShark which is integrated with GNS3 on their completed lab from Lab 6. 

### Lab 10: Packet Tracer pt 2 (debating)
