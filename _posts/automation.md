---
author: Declan Wade
tags: [homelab, automation]
title: Automating with Ansible
description: I wanna do as little as possible
date: 2023-01-21
layout: post
blog: true
---

My aim with my Homelab is to recover or setup from a fresh installation as possible. Ansible has always had an attraction as being a popular automation platform that can achieve a lot fairly easily, but as one would imagine, it is somewhat overwhelming with the scope and scale.
However, with a bit of persistence, it turns out it is rather simple and straightforward.

## Getting Started

This is probably not a great tutorial of best practices for using Ansible, but I hope it provides a simple example. 
I spent quite a while considering options for the control node, which is the device that will actually run Ansible to send the commands. This is the beauty of Ansible, it only needs to be installed on the control node, the clients or targets just need to be accessible over SSH. 
I decided that, in a scenario where no server is available, my desktop PC can act as a temporary control node. Using WSL2, I just needed Ubuntu installed and Ansible installed on top of that using the instructions at [this link.(https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)]

## The Inventory File

There are two files needed for a basic configuration, the first being an inventory file to tell which nodes to configure:
inventory.ini
```
[debian11]
10.1.1.10
10.1.1.20
```

## The Playbook:

The second file is the actual one that does the work. This is where you define the tasks and actions to run on the hosts. 
This simple example just runs ```sudo apt update``` and ```sudo apt upgrade -y``` as is fairly typical for distros which use APT package manager. 

```
- name: Prepare all
  hosts: all  
  tasks:

  - name: update and upgrade APT
    become_method: sudo
    become: true
    apt:
      upgrade: yes
      update_cache: yes
 ```
 
