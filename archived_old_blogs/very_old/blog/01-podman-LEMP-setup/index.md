---
author: Pratik Chandlekar
pubDatetime: 2023-01-27T17:05:16Z
title: "Podman pod setup for LEMP stack"
postSlug: "podman-pod-setup-for-lemp-stack"
featured: false
draft: true
tags:
  - devops
ogImage: ""
description: Using Podman pod to create a development and production setup for LEMP stack
---

## Table of contents

## Introduction

## What is podman

### Comparison with docker

### Pod

## Project Structure

## LAMP Stack

## LAMP Development Setup

## LAMP Production Setup

Create a pod:

```
podman pod create --name LEMP --publish 8080:80 --publish 3306:3306
```

Build a php image:

```
podman build -t php_lemp .
```

Run the php container inside pod:

```
podman run \
--pod LEMP \
-v $PWD/data:/var/www/html \
--privileged \
--restart=on-failure \
-d localhost/php_lemp:latest
```

Build a nginx image:

```
podman build -t nginx_lemp ../ --file Dockerfile
```

Run the nginx container inside pod:

```
podman run \
--pod LEMP \
-v $PWD/data:/var/www/html \
--privileged \
--restart=on-failure \
-d localhost/nginx_lemp:latest
```

Run MySQL container inside pod:

```
podman run \
--pod LEMP \
-e MYSQL_ROOT_PASSWORD=1234 \
--restart=on-failure \
-d mysql
```

Run phpmyadmin container inside pod:

```
podman run \
--pod LEMP \
--name phpadmin_lemp \
-e MYSQL_ROOT_PASSWORD=1234 \
-e PMA_HOST=127.0.0.1 \
-e PMA_PORT=3306 \
--restart=on-failure \
-d phpmyadmin
```

- What is Podman
- Podman vs docker
- podman pod
- PHP Nginx MySQL
- Project structure
  - php
    - php fpm
    - redirection of .php files
    - creation of php image
    - running php image with volumes mounted for development
  - Nginx
    - What is nginx
    - nginx config
    - nginx image -> container inside pod
  - MySQL
    - changes in php for my sql credentials
    - mysql image -> container in pod

## Conclusion
