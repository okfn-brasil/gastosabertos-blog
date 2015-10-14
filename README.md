wordpress-docker
===========

Developing and deploying Wordpress with Docker, an http://appcivico.com/ implementation.

> this is a fork of https://github.com/jbfink/docker-wordpress but with some different directories and configuration.

---
# Usage for deploy a new instance

1. Clone this repository and walk into the directory.
1. You should edit docker-compose.yml and change where you want to persist the data. default to ../data-mount
1. `./build-images.sh`     # build the Dockerfiles (go take a coffee)
1. `docker-compose up --no-recreate -d`

### CKAN instance mounts

- ../data-mount-wordpress/var-lib-mysql:/var/lib/mysql/
- ../data-mount-wordpress/var-www:/var/www


> WARNING: you need an initialized database on /var/lib/mysql/ otherwise:

- start docker without mounting mysql directory
- setup your wordpress
- docker exec -it $CONTAINERNAME /bin/bash
- stop the mysql
- copy the database TAR somwhere in /var/www (so it's mounted)
- shutdown docker
- copy and extract database TAR to var-lib-mysql
- start mounting mysql directory.

---

## Running commands inside the container

The simplest thing to do is to use the `docker exec` command, for example:

    docker exec -it NAME_OF_CONTAINER /bin/bash

## Managing Docker images & containers

You should use docker-compose to manage your containers & images, this will ensure they are started/stopped in order

If you want to quickly remove all untagged images:

    docker images -q --filter "dangling=true" | xargs docker rmi

If you want to quickly remove all stopped containers

    docker rm $(docker ps -a -q)

---

# Sources
- [Docker](https://www.docker.com)
- [Docker-compose](http://docs.docker.com/compose/)
