---
title: Install Docker on Ubuntu Server 18.04
date: 2018-10-21 13:07:05
updated: 
type: post
tags: [docker, containers, ubuntu, server]
---

I've had Docker on my list of tech to learn for a little while now. It seems to be an increasingly important skill to possess in 2018.

I like to self-host alternatives to popular web applications where possible. Not just because I like to think about my privacy online and control my own data, but also because it helps me learn new technology. Docker is a prime example of that. My plan over the next couple of weeks, is to to host a number of services on a VPS and make use of Docker in the process. I'll blog about that in due course, but for my own benefit and anyone who reads my blog I thought I'd write a "Getting Started" post for installing Docker on Ubuntu Server. It really is easy, so there's nothing stopping you from playing around with it in the safety of a virtual machine.

So, without further to do let's dive in...

## Prerequisites

You'll need the following to follow along with this article:

- A VM or machine running an already setup version of [Ubuntu Server 18.04](https://www.ubuntu.com/download/server)

## Adding the Docker Repositories

For personal use we need to use _Docker Community Edition (CE)_, as opposed to the _Enterprise Edition (EE)_.

Docker's own documentation lists a [number of ways](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce) you can install Docker on Ubuntu, but the easiest way in my opinion is to use the Docker repositories. This makes updating Docker easier, so for now that'll do just fine.

We're going to need to install some packages to allow Ubuntu's `apt` to use a repo over _HTTPS_. So, on your Ubuntu server, run the following.

```shell
$ sudo apt update
```

Once updated, we can install the below packages.

```shell
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

We can now add Docker's official [GPG](https://gnupg.org/) key. To do this we'll use the `curl` program and add it to our list of trusted keys used by `apt` to authenticate packages.

```shell
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

You can check you have the right key, by using `apt-key list` and making sure the Docker key is listed as below.

![2018-10-21_13-51](/images/2018-10-21_13-51.png)

We're now going to add the Docker repository to our server.

We'll be adding the stable repository. Docker's documentation says you must always use the "_stable repository, even if you want to install builds from the edge or test repositories as well._" You can add _edge_ and _test_ repositorys by adding those words below, after `stable` if you need them.

```shell
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

## Installing Docker

Lets update `apt` again now that we have added the Docker repository.

```shell
$ sudo apt update
```

We can now install Docker. Woohoo! Just run the below.

```shell
$ sudo apt install docker-ce
```

Type `y` to confirm.

![2018-10-20_18-10](/images/2018-10-20_18-10.png)

Docker should now be installed, and configured to start on boot, but we can check by doing the following.

```shell
$ sudo systemctl status docker
```

All being well you'll get an output like the below. If you see `active` under _Active_ then you are good to go, Docker is up and running!

![2018-10-20_18-17](/images/2018-10-20_18-17.png)

We can verify everything is working correctly by running the Docker `hello-world` image.

```shell
$ sudo docker run hello-world
```

According to the Docker docs this will download a test image, run it in a container and then when that container runs, it prints out everyone's favourite message!  
You can see the output below. You'll notice it couldn't find the image locally, so it downloaded it. Make sure you read the output, as it's helpful to understand what's actually happened.

![2018-10-20_18-24](/images/2018-10-20_18-24.png)

## Conclusion

That's it, simple as that. You can now start running containers with Docker, and learning more - which is what I'll be doing!
