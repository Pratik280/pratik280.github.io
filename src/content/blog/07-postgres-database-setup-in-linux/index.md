---
author: Pratik Chandlekar
pubDatetime: 2023-06-01T17:05:16Z
title: "Mastering PostgreSQL Database Setup in Docker: Persistent Volumes, User Creation, Backup, and Restoration"
postSlug: "mastering-postgresql-database-setup-in-docker-persistent-volumes-user-creation-backup-and-restoration"
featured: false
draft: true
tags:
  - linux
  - db
  - devops
ogImage: ""
description: Learn how to set up a PostgreSQL database in Docker, ensure data persistence, create users and databases, and perform backups/restorations using pg_dump. Master containerized database management.
---

## Introduction

Welcome to my blog where I dive into the world of PostgreSQL and Docker! In this article, I will guide you through the process of setting up a PostgreSQL database using Docker, leveraging volumes for data persistence. We will explore creating users and databases, and I will walk you through the steps of backing up and restoring your database using the powerful pg_dump utility. By the end of this blog, you'll have a solid understanding of how to work with PostgreSQL and Docker, ensuring data persistence and efficient management of your database environment. Let's get started on this exciting journey!

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

### Creation of tables and the insertion of values into them.

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

### Working with pg_dump to Create a Database Backup

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

### Deleting the postgres-container and Recreating It with the Same Volume to Verify Data Persistence

First stop the running docker container:

```bash
docker stop postgres-container
```

Now delete the running docker container:

```bash
docker rm postgres-container
```

To ensure data persistence and verify the presence of all data (databases, users, tables, and rows), let's start a new container using the same named volume, `postgres-container-data`, that was utilized by the previous container.

```bash
docker run -d \
 --name postgres-container \
 -e POSTGRES_PASSWORD=mysecretpassword \
 -v postgres-container-data:/var/lib/postgresql/data \
 postgres
```

Now connect to the same database `employeedb` with the same user `db user`:

```bash
docker exec -it postgres-container psql -U dbuser -d employeedb

employeedb=> SELECT * FROM public.employees;
 emp_id |   emp_name
--------+---------------
      1 | John Doe
      2 | Jane Smith
      3 | David Johnson
      4 | Emily Brown
      5 | Michael Davis
(5 rows)
```

The data persistence of our container is demonstrated by the fact that even after deleting and recreating it with the same volume, all our previously created databases, users, tables, and rows remain intact. This confirms that Docker volumes effectively preserve our data across container lifecycles.

## Conclusion

In conclusion, we have explored the process of setting up a PostgreSQL database in a Docker container, utilizing volumes to ensure data persistence. We learned how to create users and databases within the PostgreSQL environment, enabling efficient data management. Additionally, we delved into the powerful pg_dump utility, which allows us to create backups of our databases and restore them as needed. By following these steps, you now have the knowledge and tools to confidently work with PostgreSQL in a Dockerized environment, ensuring the integrity and availability of your data. Docker and PostgreSQL make a powerful combination, providing flexibility, scalability, and ease of use. I hope this blog has been informative and helpful in your journey of working with PostgreSQL and Docker.
