---
comments: true
date: 2010-06-05 20:54:19
layout: post
slug: booting-windows-7-from-an-existing-partition-inside-ubuntu-virtual-box
title: Booting Windows 7 From An Existing Partition Inside Ubuntu Virtual Box
summary: A quick guide on how to boot a windows partition on your hard-drive from an Ubuntu installation located on another partition on the same drive.
wordpress_id: 104
image: 'booting-windows-7-from-an-existing-partition-inside-ubuntu-virtual-box/windows_ubuntu.png'
tags:
- Linux
- ubuntu
- virtual box
- windows 7
---

#####  Booting Windows 7 From An Existing Partition Inside Ubuntu Virtual Box

Ok, this week presented a hell of a problem. Set up my laptop to dual boot Windows 7 and Ubuntu 10.04 Lucid Lynx. I've been using it pretty successfully as my development environment for about a week now, but something was annoying the hell out of me, every time I want to get into my Windows 7 installation for something I had to close down Ubuntu, restart the laptop and boot into Windows then do the same to get back to Ubuntu. Needless to say, tedious!

After some Googling I found the easiest way to do what I wanted, boot my existing windows partition in a virtual machine on Ubuntu, was to use VMWare Workstation. Problem, not free! Great. After another hour of Googling I came across Virtual Box and a way of booting from an existing partition.

Firstly install Virtual Box, I'm only going to explain the easy way here, go to the Ubuntu Software Center (under applications) and search for VirtualBox OSE. Install it.

Once it's installed open a terminal and do the following.

    sudo usermod -a -G disk {your_user}
    VBoxManage internalcommands createrawvmdk -filename /home/{your_user}/Documents/Windows7.vmdk -rawdisk /dev/sda -register

You should then see the following confirmation screen.

    VirtualBox Command Line Management Interface Version 1.5.0
    (C) 2005-2007 innotek GmbH
    All rights reserved.
    RAW host disk access VMDK file /home/{your_user}/Documents/Windows7.vmdk created successfully.

If you now set up a virtual machine and set the drive as the vmdk you have just created you'll be able to boot up your main hard drive and Windows 7. IO APIC and VT-x/AMD-V both need to be enabled to run a Windows Guest Operating System. These options can be found in your virtual Machine Settings on the advanced tab. However, if you're unlucky just like me you'll get to the main windows 7 loading screen and get a blue screen of dead, great. However, a further 2 hours of googling and I stumbled across the following file.

## [Merge IDE (2.5kb zip)](/img/posts/MergeIDE.zip)

Open this in Windows 7, as always before editing the registry do a backup! Run the included batch file, then run the registry file. go back to Ubunutu and try the virtual machine again. This solved the BSOD problem for me and i now have a perfectly booting virtual machine of my existing Windows 7 partition. Result!
