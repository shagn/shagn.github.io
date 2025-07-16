---
title: "Docker" 
date: "2025-04-03" 
tags: ["wip"]
draft: false
---

## General

```bash
sudo service docker start/restart/stop

# cleaning up
docker system prune # removes all stopped containers, unused networks, dangling images, and build cache
docker system prune -a # remove all unused images, not just dangling ones

# delete all images 
docker rmi $(docker images -q)
```

## Build an image

```bash
docker build -f <dockerfile> -t <name> .
docker build -f <dockerfile> -t <name>:<tag> .
```

- `-f`:allows specifing a dockerfile outside the location
- `.`: the positional argument is the build context, here `.` (= the current working directory)[^docker-cli-build]

## Run an image

```bash
docker run --rm -it -d --privileged=true -v $(pwd)/../..:/directory_in_container --name <container_name> -p 8000:8000 <image_name>:<tag e.g. latest>
```

- `--rm`: will remove existing container
- `-it`: for interactive access e.g. bash
- `--detach`/`-d`: run container in background and print container ID, no print out
- `--entrypoint`: specificy entrypoint e.g. _/bin/bash_
- `-v`: mount volume into container
- `-p`: port forwarding
- `-v`: hosting directory in container

## Manipulate running container

```bash
# use bash in a running container
docker exec -ti <container_name> bash

# get the ID of a running container
docker ps --filter ancestor=<image_name> --format "{{.ID}}"

# copy files out of a docker container 
docker cp <container id>:/file/path/within/container /host/path/target  # e.g. docker cp e9e8acdb0440:/project/geo-countries/data/countries.geojson ~/Downloads

# stopping running image
docker container stop <id>
docker container stop <tag>
```

## Transfer an image

```bash
docker save <image_name> # saved as .tar
docker save <image name>:2 | gzip > file_name.tar.gz # with gzip

docker load < file_name.tar.gz
```

## Docker Compose

Docker Compose is a tool for defining and running multi-container applications based on the YAML based compose file.

Example compose.yml

```yaml
services:
  caddy:
    image: caddy:2.10
    restart: unless-stopped  # container will start unless deliberately stopped by the user
    ports:
      - "80:80"
      - "443:443"
      - "443:443/udp"
    volumes:
      - ./conf:/etc/caddy  # maps a local directory ./conf on the host machine to /etc/caddy inside the container
      - caddy_data:/data  # creates a named volume `caddy_data` mapped to `data` in the container. Named volumes are managed by Docker and persist even when containers are removed
```

## References

[^docker-cli-build]: https://docs.docker.com/reference/cli/docker/build-legacy/
