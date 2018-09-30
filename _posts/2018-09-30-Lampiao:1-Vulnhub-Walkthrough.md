---
layout: post
title: "Lampião: 1 Vulnhub box Walkthrough"
img: hacker.jpg # Add image post (optional)
date: 2018-09-30 23:54:00 +0300
description: A walkthrough of intentionally vulnerable  box for beginners. # Add post description (optional)
tag: [Hack , Vulnhub_Box , Pentest]
---
Hi there, This is gonna be a walkthrough on an intentionally vulnerable box for beginners who is just starting to practice on vulnerable boxes from vulnhub. 'Lampião: 1' is an intentionally vulnerable ubuntu machine created by 'Tiago Tavares' for beginners. 

Before getting into the practice on boot2root. Let me tell you the requirments of starting practice on vulnerable machines. It's good if you have kali linux installed on your system as primary OS or Virtual Machine will also be fine. I would recommend to have virtual box installed on you system which is absolutely free of cost. Now let's download 'Lampiao:1' box from vulnhub website. Basically you get .vmdk file in a zipped folder which can be run in virtual box. Once downloaded, unzip the lampiao.zip folder and you can see 'Lampiao-disk1.vmdk' file in the folder. Now open virtualbox, you can see a 'New' button and top left corner, just click on it and go next until it takes you to finish. Once finished, you can see it in the left panel of virtualbox. Select that and click on settings button on top, go to network tab and choose 'Bridged Adapter' in 'Attached to:' section. Jump up to 'Storage' tab and under 'Controller SCSI' section you can see 'Hard Disk:' tab. You got to choose '.vmdk' file there. So navigate to Lampiao folder and 'Lampiao.vmdk' file. That's all, we are good to go. Let's now start the vm and head up to our kali machine.

Now fire up your kali machine and open up terminal to figure out the ip address of target machine using 'netdiscover' command(in my case it's 192.168.1.5). Let's now start gathering some information about the target machine. Let's scan the ports running on the machine first and for that we are gonna be using one of the best tools called 'nmap'. In order to use nmap, open terminal and type 'nmap -sV -p- ipaddress(in my case 192.168.1.5)'. So basically we are asking nmap to scan all ports by giving '-p-' command and all the running services by giving '-sV' command. Refer the screenshot.
