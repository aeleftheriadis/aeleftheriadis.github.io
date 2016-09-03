---
layout: post
title: "Docker for .net devs"
excerpt: "Docker intro for .net developers"
image: /assets/imgs/docker-whale.jpg
comments: true
categories:
  - Docker posts
tags: 
  - docker
  - .net
---

Docker is a very useful tool that simplifies the development and deploy of applications. Docker helps you package your entire application as a package with all the necessary dependencies and then deploy it on a server. Docker run everywhere Windows, Linux or Mac OSX, so you can code your application in any system you like and then deploy it as a **containered** package.

This packaged application is called **container** in Docker world. Each container is **lightweight** since it makes efficient use of RAM and shares the operating system kernel. **Secure**, since it’s isolated from the rest of the system, and adds an additional layer of security. It’s not a VM. Of course you can run Docker on a VM or bare metal but either way you have a container that it’s isolated and not tied to the underlying infastructure.

It’s opensource and you can find many images provided by community maintainers to get started with at [https://hub.docker.com/](https://hub.docker.com/){:target="_blank"}.

- - -

### Enough with the introduction. Let’s jump into a practical example



First of all you will need docker to be installed on your machine. I believe you are on Windows host so you will have to install docker toolbox. Find the instructions at [https://www.docker.com/products/docker-toolbox](https://www.docker.com/products/docker-toolbox){:target="_blank"}.

When you setup is complete start Docker Quickstart Terminal. Now you have a docker-machine with name «default» running at Virtualbox with local IP address 192.168.99.100. More about docker machine at [https://docs.docker.com/machine/](https://docs.docker.com/machine/){:target="_blank"}

Jump to [https://hub.docker.com/r/microsoft/dotnet/](https://hub.docker.com/r/microsoft/dotnet/){:target="_blank"} This is a .NET Core Docker Image

1. Let’s create a very basic app
2. Execute the following command on docker quickstart terminal `docker run -it --rm --name mydotnet microsoft/dotnet:latest`
> Docker downloads microsoft/dotnet image latest version, creates and runs the container with name mydontnet. –rm flag is used to remove any previous containers with the same name. For interactive processes (like a shell), you must use -i -t together in order to allocate a tty for the container process. *You now have a container*
3. So let’s add an app directly into the container.
> In case you haven’t noticed we have a linux command prompt starting with root. So run the following.

    `
    mkdir hello_world
    cd hello_world
    dotnet new
    dotnet restore
    dotnet run
    `



### We have created a new Hello World app and the restored all the necessary dependencies and then run the app



More samples at [https://github.com/dotnet/core/tree/master/samples](https://github.com/dotnet/core/tree/master/samples){:target="_blank"}


As a result we have run a .net core app into docker at windows. The application has a Program.cs that apparently write to the console «Hello World» and has a project.json with the necessary dependencies.

- - -

### Bonus:

There are more alternatives to install Docker on Windows.
1. Docker is building an app for Windows and Mac. Right now it’s working with with Hyper-V on Windows. So if you have Windows 10 with Hyper-V download at [https://download.docker.com/win/stable/InstallDocker.msi](https://download.docker.com/win/stable/InstallDocker.msi){:target="_blank"}
2. Setup a local Windows 2016 TP5 Docker VM with Vagrant and Packer. More at [https://stefanscherer.github.io/setup-local-windows-2016-tp5-docker-vm/](https://stefanscherer.github.io/setup-local-windows-2016-tp5-docker-vm/){:target="_blank"}

- - -

### Last tip

If you want docker command to be available on your console or powershell add the following folder C:\Program Files\Docker Toolbox to Windows PATH.

- - -

#### References:

1. [https://www.docker.com](https://www.docker.com){:target="_blank"}
2. [https://docs.docker.com/engine/reference/run](http://https://docs.docker.com/engine/reference/run){:target="_blank"}
3. [https://hub.docker.com/](http://https://hub.docker.com/){:target="_blank"}
4. [https://www.docker.com/products/docker-toolbox](https://www.docker.com/products/docker-toolbox){:target="_blank"}
5. [https://docs.docker.com/machine/](https://docs.docker.com/machine/){:target="_blank"}
6. [https://hub.docker.com/r/microsoft/dotnet/](https://hub.docker.com/r/microsoft/dotnet/){:target="_blank"}
7. [https://blog.docker.com/2016/03/docker-for-mac-windows-beta/](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/){:target="_blank"}
8. [https://stefanscherer.github.io/setup-local-windows-2016-tp5-docker-vm/](https://stefanscherer.github.io/setup-local-windows-2016-tp5-docker-vm/){:target="_blank"}