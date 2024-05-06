---
title: "Docker CLI Cheatsheet"
date: 2022-08-08T08:39:56-05:00
description: "License to Krill"
author: "Kyle Weise"
draft: false
type: "post"
showTableOfContents: false 
tags: ["Docker", "Containers", "DevOps", "Linux", "Cheatsheet"]
---

![Cover Art](/images/posts/cheatsheets/docker/cover.png)

## Basic Docker Commands

| Description | Command | Notes |
| --- | --- | --- |
| Pulls docker image from [hub.docker.com](https://hub.docker.com) | `docker pull [image name]` | |
| Runs container | `docker run [image name]:[tag]` | |
| Run container in "detached" mode | `docker run -d [image name]:[tag]` | Running as daemon/background |
| Run container on port `8000` | `docker run -p 8000:80 [image name]:[tag]` |  Format for port flag is `[host:container]` |
| Naming container | `docker run --name container-name [image name]:[tag]` | |
| Mounting a volume | `docker run -v /path/to/file/host:/where/to/put/file:[ro/rw] [image name]:[tag]` | | 
| Starting a container | `docker start [container ID/container name]` | |
| Stopping a container | `docker stop [container ID/container name]` | |
| Lists the processes of docker containers | `docker ps` | |
| Same as `docker ps` | `docker container ls` | |
| Lists installed docker images | `docker images` | Default |
| Same as `docker images` | `docker image ls` | |
| Removing a single container | `docker rm [container ID/container name]` | |
| Removing all stopped containers | `docker rm $(docker ps -aq)` | |
| Removing all containers, regardless of state | `docker rm -f $(docker ps -aq)` | |
| Builds a Docker image | `docker build -t [new image name]:[tag] .` | Dockerfile needs to be in current working directory |
| Interactive shell inside container | `docker exec -it [container ID/container name] [shell]` | |
| Outputs container info to JSON format | `docker inspect [container ID/container name]` | |
| Outputs log of container | `docker log [container ID/container name]` | |

