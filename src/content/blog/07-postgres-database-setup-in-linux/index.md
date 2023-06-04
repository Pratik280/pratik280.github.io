---
author: Pratik Chandlekar
pubDatetime: 2023-06-01T17:05:16Z
title: "Comprehensive Postgres Database Setup Guide in Linux"
postSlug: "comprehensive-postgres-database-setup-luide-in-linux"
featured: false
draft: true
tags:
  - linux
  - db
  - devops
ogImage: ""
description: Database
---

## Introduction

- Using docker for postgres databse.
  - volume
- Creating Databses
- Creating Databse dump
- Creating Databses from dump
- Creating users with encrypted password and assginging users to databases.
- hba_file
- Connecting backend applications with postgres database. (nodejs, java springboot, python flask)

sudo -u postgres psql

> \l dt c db name
> \dt

psql -U postgres -d sit_devops_config -1 -f filename.sql
CREATE USER sit-devops-config_user WITH CREATEDB CREATEROLE ENCRYPTED 'S1i2t3-devops-config_user';
\c dbname

GRANT ALL ON SCHEMA PUBLIC TO "sit-devops-config_user"
dump

psql -U sit-devops-config_user sit-devops-config < dumpfilename.sql
alter role "sit-devops-tlm_user" with encrypted password 'S1i2...'
sudo su - postgres

psql -c "SHOW hba_file;"

Doing

[Dockerhub official postgresql image](https://hub.docker.com/_/postgres)

Pull the image locally:

```bash
docker pull postgres
```

```bash
docker run --name test-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

```bash
docker exec -it bee19e7b958a /bin/bash
```

```bash
su - postgres
```

```bash
psql
```

## Conclusion
