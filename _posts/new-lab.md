---
author: Declan Wade
tags: [homelab]
title: My New Homelab
description: Windows vs Linux!.
date: 2023-01-20
layout: post
blog: true
---

As you can see from the previous post, I was running what could possibly call an 'unorthodox' homelab as it was Windows 10 Pro with Docker Desktop. 
However it has been a while and things have changed. 
Welcome back to Debian.

## Windows, what went wrong

Reliability is a big factor for me. Although it was pretty good for the most part, I did start to notice some gremlins.
Event View was full of errors with the entry "The driver detected a controller error on \Device\harddisk3\DR3 which is one of my spinning disks. There were no SMART errors on the disk, and some sites indicated this could be USB Controller issue, but the array functioned anyway. 
The real issue as the very occasional complete drop-off from the network. The computer would just go offline completely and I wasn't able to capture a video-out signal from the NUC to see if it was a bluescreen. This was a dealbreaker.

## Choice of alternative

As Docker Desktop had provided me with the experiance and knowledge with containers that I didn't have before, I wanted to try Linux again for my mission-critical server OS of choice.
Although the distro I had the most experiance with was Ubuntu, I decided to go with Debian for the rock-solid stability and familiarity. I also spun up several VMs of Debian 11 Bullseye to familiarise myself with installation and network setup. 
Some good lessons on the way was to not set a root password during setup, forcing the root user to be disabled but have ```sudo``` enabled on the non-root user.

## Setup and Migration

Compared to previous setups, I carried across a substantial amount more data across than my usual clean-slate. Most of my services were already running on Docker, thus being (mostly) host agnostic, it was a simple matter of re-mapping the bind-mounts. 
Plex was a clean slate, as the way that the data files are stored on Windows and Linux is completely different and not transferrable.
The data store was transferred across simply by using FUSE to mount the disks, maintaining the NTFS filesystem. However, a few months after the migration, I purchased two Seagate Ironwolf 6TB drives to replace the existing two 3TB Seagate Barracuda drives that I was using, effectively doubling the storage. 
For the new drives, I went with ZFS as a self-healing, highly resiliant and modern filesystem that recently got proper support from Debian. 