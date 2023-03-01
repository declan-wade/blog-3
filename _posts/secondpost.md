---
author: Declan Wade
tags: [homelab]
title: My unorthodox Homelab
description: Windows vs Linux!.
date: 2022-06-04
layout: post
blog: true
---

As someone who has been running a homelab for the past 8 years, I have had the chance to run a huge variety of hardware and software to try out different things. From memory, this has now surmounted to  CentOS, Ubuntu, Debian, FreeNAS (now TrueNAS), unRAID, Windows Server, ESXi, Proxmox and standard Windows. 

These are very different OSes for a variety of reasons, some are suited at different tasks and are more specialised than others. I want to give my pros and cons on using Linux and Windows, as running Windows on a budget homelab isn’t as common as one might think. 
These pros and cons are my personal opinion - I know some people will consider some of my cons a feature that they like about the OS, but this is just my experience. 

## Having the flexibility of a desktop environment is great. 

Although I am familiar with the basics of the Linux CLI, I am still more comfortable using a GUI especially for certain tasks. I have used desktop based distros before like Ubuntu, Xubuntu, Rocky Linux, Fedora and Debian, however the sticking point for me is getting Remote Desktop (VNC) to work reliably. The number of hours I have spent getting VNC to work on Ubuntu is maddening, with no less help from the internet which seems to have dozens of different ways of approaching the issue (very much dependant on the type of environment your using and the version of the OS - the implementation keeps changing!). On Windows, even the most advanced options are accessible via a GUI, and RDP is fast, reliable and easy to turn on. 

## Pricing sort of matters. 

Linux is free, at least for the vast majority of distros. Windows definitely is not free, but can be found for as little as AUD$40 - $50 for an OEM license. Microsoft is also taking a fairly relaxed approach to upgrading Windows 10 to 11 with whatever license you are currently using on your hardware. 
If you have additional requirements such as a dual socket motherboard/CPU, then you would need to use Windows Server which becomes even more expensive. 

## Reliability 

From my limited experience, it is hard to beat the legendary reliability of many Linux Distros. I have had a host of issues in the past with blue screens and stability issues on Windows that can make for a rather frustrating experience. If you have a solid recovery plan with a reliable backup solution, this becomes less of a problem - so far I have had fairly solid reliability with the latest build of Windows 11 Pro on a Intel NUC8 i5, but the same can’t be said for when I tried to add an additional 16GB of RAM. 

## WSL2 has unlocked a lot of power and flexibility 

Windows Subsystem for Linux (WSL) was introduced initially in 2016, effectively as a Bash shell, aiming for ‘native Linux’ on Windows at a kernel level - however it had limited application as it didn’t include the ability to run system services or daemons. 
WSL2 was introduced in 2019 and is completely re-architected with the entire Linux kernel running in a special lightweight Hyper-V based VM, while still maintaining deeper integration with Windows processes. 
While it was previously possible to run Docker on Windows, I found it slow, unreliable and buggy. With the introduction of Docker Desktop running on the WSL2 layer, it has significantly improved performance and reliability to make Docker a very viable solution on Windows. 
Let’s take an example. 
NextCloud is a very popular self-hosted file sharing and collaboration platform, however there is no ability to run the server on Windows (unless you use a VM) which could be a dealbreaker for those who need to run Linux services or servers. 
Rather than mucking around with spinning up VMs, NextCloud can now be simply run with a docker-compose file. 
There are limitations to Docker on Windows for some of the more advanced features and edge cases, but I am currently running 39 containers with only 16GB of system RAM - imagine doing that with VMs!

## Storage

The other constraint with Windows is the lack of flexibility with file systems, at least without a substantial amount of additional work. This means no native support for ZFS or BTRFS for either the OS or external drives. Microsoft has a new file system named ReFS, but this is relatively new with some concerns around stability, plus can only be used on Windows Server or Windows 10 Enterprise or Pro for Workstation (not regular Pro) and thus I am stuck with NTFS, which will soon have its 30th birthday…
There is a binary being developed by OpenZFS to provide a ‘port’ of ZFS on Windows, but it is in very early development. 
For me - NTFS is ‘good enough’ to not be an issue, but it should be a consideration when deciding the architecture of your homelab. 

## Conclusion

I hope some of the information above is useful for those who are exploring the world of starting their own homelab. It’s always a great idea to just try and try and try again with different OSes to get a feel of what works for you. 