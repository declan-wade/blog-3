---
author: Declan Wade
tags: [homelab, docker]
title: Docker Run CLI reference
description: Let's try a basic example to run Docker containers
date: 2022-05-01
layout: post
blog: true
---

## An easy guide for simple Docker run syntax

`DISCLAIMER: this guide represents an over-simplified reference of the Docker syntax and does not represent best practices or a comprehensive use of the CLI`

This example is one of the most basic type of commands used for the Docker ‘run’ command, which should provide a fundamental understanding of being able to use Docker in real world applications. However, this is not the bare minimum in terms of running a container, although it does provide a good starting point for useful containers that have real world applications. 

Take this simple example:

On Windows:

`docker run -d -p 8080:80 —name my-apache-php-app -v C:\Docker\My_App:/var/www/html php:7.2-apache`

On Linux:

`docker run -d -p 8080:80 —name my-apache-php-app -v ~/my_app:/var/www/html php:7.2-apache`

Let’s break this down

The first bit `docker run` is obviously the CLI command that you want to run a new container. This means it will download and then try to run the container immediately. 

The next part is the `-d` which is the “detached” flag. This means that upon completion of the command, it will return back to your shell. If you do not run include the flag, the shell will start to return the logs of the container as applicable. This can be useful but closing the shell while in the attached mode will stop the container. I find it generally easier to monitor the container using Docker Desktop or using the `docker logs` command, which we will cover in a different guide. 

Naming the container can easily be done by using the `—name` flag. You should try and use a name without spaces or special characters. You can run the container without specifying a name, however the daemon will give the container a random dictionary name, which makes it hard to know what you’re running. 

The next part is the `-p 8080:80` is the “port” flag. The number **before** the colon refers to the port you wish to be opened on the host, while the number **after** the colon refers to the port inside the container. As a general rule of thumb, the host port can be anything you want provided it doesn’t conflict with an existing open port, while the container port should be the same as the documentation provided by the container developer. 

The next part is the `-v` or “volume” flag, which varies between Windows or Linux depending on your host. The use of volumes are very useful for containers they need to access data such as media folders, or providing “persistent” data. Without specifying a volume, all data will be lost when the container is removed. In almost all instances, not the whole container is mapped (i.e. from the root / folder down) - rather just the necessary components that contains configuration or data. This modular approach allows containers to be easily updated, while also providing a simple way to allow a persistent configuration. 

The following diagram provides a simple example in Windows:



As we have used the flag `C:\Docker\My_App:/var/www/html` this has now bound the two locations together - any change made in one is reflected in the other. 
Sometimes, you need to put data in this location (such as a config file) before starting the container, as the container will be relying on this data to get the information it needs. Other times, the container will create its own files and folders, which you can then edit. 
Regardless of how the files and folders are created, they exist until such time they are either deleted by the user or in rare circumstances, by the container. 

The last key component is the image, which is at the end of the command and basically tells which image you want to create the container from. Many container images can be found from the Docker Hub, although they can be hosted in other locations as well. The image name is specified, then sometimes by a tag. In this example, the name of the image is `php`and the tag is `7.2-apache`‌. Tags are often used to select a specific type of image or version depending on the repository. Many repositories recommended using the latest tag to ensure you are running the latest build. This one is specifying a specific version of PHP - 7.2 running on Alpine Linux. 

There are a range of other flags we haven’t covered in this guide, but will be touched on in the future.   