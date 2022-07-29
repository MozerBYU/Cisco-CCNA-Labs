# IT-C 347 Labs
## Brigham Young University - IT & Cybersecurity Program

These labs are for the IT-C 347 - Networking class, taught in the Fall 2022 Semester.

## Lab Structure

There are 9 labs in total. Labs 2 - 9 are divided in two parts: part a which is conceptual, and part b which is practical. This allows students the ability to learn the concept and have a few write-up questions to test their understanding, and then put that knowledge into practice to solidify it.

### Lab 1: Intro: Setup Cisco Academy and GNS3

In this lab, students setup an account with Cisco Academy and with GNS3. They will then install VMWare Workstation Pro to run the GNS3 VM that we will run our lab in.

### Lab 2: Networking Cabeling Basics

In this lab, students will get hands-on practice in creating Cat 5e patch cabeling, and performing terminations to network jacks and patch panels. They will also learn about the standards surrounding the various generations of ethernet cabeling from Cat 1 to Cat 7. 

### Lab 3: IPv4 Addressing and Subnetting

In this lab, students learn about the differences between public IPs and private IPs, how IPv4 classes are setup and the standards surrounding them, and those IP classes relate to classless and classful IP ranges. They will also learn a basic understanding of how gateways and routers help packets get around the internet. Finally, they will learn how subnetting works. How to segregate a larger network into smaller sub-networks using CIDR notation, and how point-to-point links function.

In the practical lab, at this stage the students will setup is the individual hosts on their respective subnets.

The completed lab, to this point, should look like the following:

![Completed Lab 3](/assets/images/gns3/Lab-3.png "Completed Lab 3")

### Lab 4: Switches

In this lab, students will get hands-on practice will a live Cisco switch. In the lab they will learn how to reset a password on a switch, and upgrade the firmware for said device. Additionally, they will learn about how switches operate and how switching tables function.

In the practical lab, at this stage the students will then take those hosts from the last lab, and connect them to switches. All hosts should be able to talk within their respective subnets.

The completed lab, to this point, should look like the following:

![Completed Lab 4](/assets/images/gns3/Lab-4.png "Completed Lab 4")
 
### Lab 5: VLANs

In this lab, students will learn about the OSI Model, what VLANs are, why they are so useful, how they work, how ethernet frames are setup, and how VLANs relate with subnetting.

In the practical lab, at this stage the students will then put those hosts into their respective VLANs. All hosts should be able to talk within their respective subnets and within their respective VLAN (including across subnets).

The completed lab, to this point, should look like the following:

![Completed Lab 5](/assets/images/gns3/Lab-5.png "Completed Lab 5")

### Lab 6: Routers

In this lab, students will learn about how routing works, how routing tables function, how to create and setup static routes, and how to implement point-to-point links.

In the practical lab, at this stage the students will then connect all switches to two respective distribution routers. Using static routes, they will make it so that hosts can talk from one router to another. ALl hosts should be able to talk within their respective subnets, vlans and talk across vlans. The lab will be tested for completion and then passed-off.

The completed lab should look like the following:

![Completed Lab 6](/assets/images/gns3/Lab-6.png "Completed Lab 6")

### Lab 7: Advanced Networking Technologies (optional)

The purpose of this lab is to introduce students to more advanced routing technologies, like OSPF. As this is more advanced, this lab is optional for students. But is a good preparation for the IT-C 529 - Advanced Networking class if they choose to take it.

In the practical lab, students will go back to their completed lab, they will add two core routers and one more distribution router with two more switches and a few more hosts in VLANs of their choosing. They will go to the original distribution routers and remove the static routes they set up. They will then implement OSPF areas and communication between each distribution router and core router. 

The complete lab should look like the following: 

### Lab 8: Network Troubleshooting

In this lab, students will get hands-on practice with doing network troubleshooting. Students will work in teams for this lab to get them accustomed to working on a IT team in the real-world. They will be given a pre-broken lab, and will need to see if they can figure out what is wrong and get it working again in functionality similar to their completed lab at the end of Lab 6.

### Lab 9: Packet Tracer

In this lab, students will get hands-on practice doing packet tracing using WireShark which is integrated with GNS3 on their completed lab from Lab 6. 

### Lab 10: Packet Tracer pt 2 (debating)
