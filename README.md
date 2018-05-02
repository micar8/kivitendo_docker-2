kivitendo_docker
================

Docker Build for Kivitendo a erp solution for small businesses.
 - Ubuntu:14.04
 - Postgresql 9.3
 - Kivitendo 3.5.0

# Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
    - [Data Store](#data-store)
    - [Securing the server](#securing-the-server)
- [Upgrading](#upgrading)
- [Start](#start)

# Introduction

Dockerfile to build a Kivitendo container image which can be linked to other containers.
Will install Postgres and Apache2 and all the necessary packages for Kivitendo.


# Installation

Pull the latest version of the image from the docker index. 

```bash
docker pull micar8/kivitendo_docker-1
```


# Quick Start

Run the Kivitendo image

```bash
docker run --name <name_of_your_container> -d micar8/kivitendo_docker-1
```
Check the ip of your docker container
```bash
docker ps -q | xargs docker inspect | grep IPAddress | cut -d '"' -f 4
```

Got to the administrative interface of kivitendo using the password: admin123 and configure the database. All database users (kivitendo and docker) use docker as password.

To test if the postgresql server is working properly, try connecting to the server.

```bash
psql -U postgres -h $(docker inspect --format {{.NetworkSettings.IPAddress}} <name_of_your_container>)
```

# Configuration

## Data Store

For data persistence a volume should be mounted at `/var/lib/postgresql`.

The updated run command looks like this.

```bash
docker run --name <name_of_your_container> -d \
  -v /opt/postgresql/data:/var/lib/postgresql micar8/kivitendo_docker-1:latest
```

This will make sure that the data stored in the database is not lost when the image is stopped and started again.

## Securing the server

By default 'docker' is assigned as password for the postgres user. 

You can change the password of the postgres user
```bash
psql -U postgres -h $(docker inspect --format {{.NetworkSettings.IPAddress}} <name_of_your_container>)
\password postgres
```


# Upgrading

To upgrade to newer releases, simply follow this 3 step upgrade procedure.

- **Step 1**: Stop the currently running image

```bash
docker stop <name_of_your_container>
```

- **Step 2**: Update the docker image.

```bash
docker pull micar8/kivitendo_docker-1:latest
```

- **Step 3**: Start the image

```bash
docker run --name <name_of_your_container> -d [OPTIONS] micar8/kivitendo_docker-1:latest
```


# Start

Browser: http://"ipadress":"port"/kivitendo-erp/
