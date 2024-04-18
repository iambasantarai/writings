---
title: CentOS setup with docker
date: 2024/04/18
description: Simple Dockerfile for setting up a basic CentOS image
tag: 8th sem, Network and System Administration
author: Basanta Rai
---

# CentOS setup with docker

Welcome! In this guide, we'll walk through setting up a CentOS Docker image for basic network administration tasks.

### What you need

A computer with [docker](https://www.docker.com/) installed

## Getting started

1. **Creating a directory**

First, let's create a directory to work in. Open your terminal or command prompt and execute the following command:

```sh
mkdir nsa
```

This command will create a directory named `nsa`.

2. **Navigating to the Directory**

Once the directory is created, navigate into it:

```sh
cd nsa
```

Now you're ready to proceed with setting up the CentOS Docker image.

3. **Creating a docker file**

Let's start by creating a file called `Dockerfile`. You can do this in any text editor.
Copy and paste the following content into `Dockerfile`.

```dockerfile
# Use the official CentOS 7 base image
FROM centos:centos7

# Update packages and install necessary dependencies
RUN yum -y update && \
    yum -y install \
    net-tools \
    && yum clean all
```

4. **Building the docker image**

Open your terminal or command prompt and navigate to the directory containing the `Dockerfile`.
Run the command below to build the Docker image. It may take a few moments.

```sh
docker build -t centos .
```

5. **Running the docker container**

Once the image is built, it's time to run a container from it. Use the following command:

```sh
docker run -it centos
```

This command launches an interactive session in a new container based on our CentOS image.

6. **Testing network commands**

You're now inside the CentOS container. Let's test some network commands to ensure everything is working as expected.

Run the following commands to check network configurations:

```sh
ifconfig
```

```sh
route -n
```

These commands will display network interfaces, and routing tables respectively.

7. **Exiting the container**

Type `exit` and hit Enter to leave the container.
