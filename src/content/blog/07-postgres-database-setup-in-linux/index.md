---
author: Pratik Chandlekar
pubDatetime: 2023-06-01T17:05:16Z
title: "Comprehensive Postgres Database Setup Guide in Linux"
postSlug: "comprehensive-postgres-database-setup-luide-in-linux"
featured: false
draft: false
tags:
  - linux
  - db
  - devops
ogImage: ""
description: Database
---

## Introduction

In this article we will be creating a database in postgresql from scratch with a user and encrypted password. Postgreql we be running in a docker container and the data will be stored on a local physical machine using docker volumes. We we also learn some basic psql commands and learn about importing and exporting the data using pg-dump. Then we will connect a simple backend sever application with postgresql database.

## Using docker for postgres databse.

We will be using the [Dockerhub official postgresql image](https://hub.docker.com/_/postgres) to run our postgres database server.

To pull the image locally run the following command:

```bash
docker pull postgres
```

Start the postgres database container using the following command:

```bash
docker run -d \
 --name postgres-container \
 -e POSTGRES_PASSWORD=mysecretpassword \
 -v postgres-container-data:/var/lib/postgresql/data \
 postgres
```

Let's break down the command and its options:

- `--name postgres-container` sets the name of the container as "postgres-container".
- `-e POSTGRES_PASSWORD=mysecretpassword` is an environment variable which is used to set the password for the PostgreSQL instance running inside the container.
- `-d` runs the container in the background (detached mode), so it doesn't occupy the terminal session.
- `-v postgres-container-data:/var/lib/postgresql/data` is a option that creates a volume named "postgres-container-data" and mounts it to the directory /var/lib/postgresql/data within the container. Volumes allow persistent storage, so the data stored in that directory will be preserved even if the container is stopped or removed. This is commonly used to store the database files and ensure data persistence.
- `postgres` is the docker image(pulled locally earlier) which will be used to create the container.

```bash
docker exec -it postgres-container /bin/bash
```

Let's break down the command and its options:

- `docker exec`: This is the command to execute a command within a running Docker container.
- `-it`: These options allow for an interactive session with the container. It combines the -i (interactive) and -t (pseudo-TTY) options.
- `postgres-container`: This is the name or ID of the Docker container where you want to execute the command.
- `/bin/bash`: This is the command you want to run inside the container. In this case, it starts a Bash shell within the container.

The prompt will change and our shell we will be inside the container:

Now run the following command to switch to the `postgres` user:

```bash
su - postgres
```

The psql command is used to interact with a PostgreSQL database from the command line. It provides an interactive terminal-based interface for executing SQL queries and managing the PostgreSQL server.

```bash
psql
```

### Some basic psql commands that are necessary to know before working with psql:

- `\l`: Lists all available databases.

- `\c <database_name>`: Connects to a specific database.

- `\dt`: Lists all tables in the current database.

- `\d <table_name>`: Shows the structure of a specific table.

Now we will create a user using `CREATE USER` command in PostgreSQL which is used to create a new user account with specified attributes, including an encrypted password.

```sql
CREATE USER dbuser WITH ENCRYPTED PASSWORD 'dbuser123';
```

Let's break down the CREATE USER command:

- `CREATE USER`: This is the command used to create a new user in PostgreSQL.
- `dbuser`: This is the username we have assigned to the new user.
- `WITH ENCRYPTED PASSWORD`: This clause specifies that you are providing an encrypted password for the user.
- `'dbuser123'`: This is the encrypted password for the user.

Let's proceed with creating a new database and designating `dbuser` as its owner.

```sql
CREATE DATABASE employeedb OWNER dbuser;
```

Use the following command to list all databases:

```psql
\l
```

Now connect to the `employeedb` database as user `dbuser`:

```psql
\c employeedb dbuser
```

For the purpose of demonstration, we will proceed to create a few tables in the `employeedb` database.

```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(255)
);
```

```sql
CREATE TABLE designations (
  designation_id INT PRIMARY KEY,
  designation_name VARCHAR(255)
);
```

Adding few rows in the tables

```sql
INSERT INTO employees (emp_id, emp_name)
VALUES
  (1, 'John Doe'),
  (2, 'Jane Smith'),
  (3, 'David Johnson'),
  (4, 'Emily Brown'),
  (5, 'Michael Davis');
```

```sql
INSERT INTO designations (designation_id, designation_name)
VALUES
  (1, 'Manager'),
  (2, 'Engineer'),
  (3, 'Analyst'),
  (4, 'Developer'),
  (5, 'Administrator');
```

To retrieve all the rows stored in the table and display them:

```sql
SELECT * FROM employees;
SELECT * FROM designations;
```

To create a dump file of a PostgreSQL database, you can use the following command:

```bash
pg_dump -U <username> -d <database_name> -f <dump.sql>
```

As we are running PostgreSQL inside a Docker container, we need to modify the command accordingly.

```bash
docker exec -t <container-name/container-id> pg_dump -U <db-user> -d <db-name> > <output-file>
```

```bash
docker exec -t postgres-container pg_dump -U dbuser -d employeedb > dump.sql
```

We will now proceed to delete the employeedb database and then recreate it using the previously created dump file. Please note that before creating the database from the dump file, it is necessary to add the user specified within the dump file.

```bash
DROP DATABASE employeedb;
```

To recreate a database using a dump file, it is necessary to first create the database that is referenced within the dump file.

```sql
CREATE DATABASE employeedb;
```

```sql
GRANT ALL PRIVILEGES ON SCHEMA public TO dbuser;
```

The command below is utilized to import/recreate a database by utilizing a dump file.

```bash
psql -U your_username -d your_database_name -f your_dump_file.sql
```

As we are running PostgreSQL inside a Docker container, we need to modify the command accordingly.

```bash
docker exec -i <CONTAINER_ID> psql -U <db-username> -d <db-name> < dump.sql

docker exec -i postgres-container psql -U dbuser -d employeedb < dump.sql
```

Once the database has been created using the dump file, you can verify its creation by examining the rows within the table.

To begin, establish a connection to the database using the following command:

```bash
docker exec -it <CONTAINER_NAME_OR_ID> psql -U <USERNAME> -d <DATABASE_NAME>
```

```bash
docker exec -it postgres-container psql -U dbuser -d employeedb
```

Subsequently, execute SELECT queries to verify the consistency of tables and their respective rows following the recreation of the database using the dump file.

```sql
SELECT * FROM employees;
SELECT * FROM designations;
```

- Connecting backend applications with postgres database. (nodejs, java springboot, python flask)

sudo -u postgres psql

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

## Conclusion
