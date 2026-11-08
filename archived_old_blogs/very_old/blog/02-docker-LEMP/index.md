---
author: Pratik Chandlekar
pubDatetime: 2023-02-04T17:05:16Z
title: "Docker-compose setup for LEMP stack"
postSlug: "docker-compose-setup-for-lemp-stack"
featured: false
draft: true
tags:
  - devops
ogImage: ""
description: Using docker and docker-compose to create a development and production setup for LEMP stack
---

## Table of contents

## Introduction

## What is docker?

## What is docker-compose & How it works?

## Project Structure

## LEMP Stack

### Nginx

[Nginx](https://www.nginx.com/) is a web server. It is a application that runs on server machine which will receive request from the internet and it will send respective respone(web pages) to it.

First I am running nginx docker container with no configuration using command:

```bash
docker run -dp 8080:80 nginx
```

The above commmand wil grab the nginx latest image from [docker hub](https://hub.docker.com/_/nginx).

**-d** - detach mode this means it will run the container in background

**-p 8080:80** - Is port binding which binds port 8080 of host machine with port 80 of container.

> Open browser and visit localhost:8080. You will se _Welcome to nginx_ default page.

List the running containers using command:

```
docker ps
```

To see the logs grab the container id from the above command and use command:

```
docker logs <container_id>
```

#### Nginx Configuration

Nginx configuration files located at /etc/nginx inside container.
**docker exec** command is used to run new command inside a container.
We can use this command to run a shell (bash,sh) inside container.
Using **-i** (--interactive) and **-t** (--tty) we can run command like:

```
docker exec -it <container_id> /bin/bash
OR
docker exec -it <container_id> /bin/sh
```

This will run a interactive shell inside container.
Then we can navigate to **/etc/nginx** directory where all the configuration files of nginx are located.

```bash
ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params
```

## LEMP Development Setup

## LEMP Production Setup

## Conclusion
