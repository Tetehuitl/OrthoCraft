---
title: The Best Way to Setup Nginx Proxy Manager
description: 
published: false
date: 2022-02-23T15:25:32.026Z
tags: 
editor: markdown
dateCreated: 2022-02-23T15:25:29.860Z
---

I recently found Nginx Proxy Manager and have found it to be much better than trying to setup a reverse proxy by hand. 

first you will need to install Docker and docker-compose.

On Ubuntu:

``` sh
sudo apt install docker docker-compose
```

## Docker Container Manager

Next you are going to want to install [Portainer](https://protainer.io)

Instructions for installing Portainer are [here](/en/portainer-install).

## Nginx Proxy docker-compose

First you need to create a network

### network

you can create the network using the command line also with the portainer interface.

```
sudo docker network create proxy
```
or with Portainer:

1. Choose Networks from the right navigation bar and then + Add Network.
1. Give it an name. (Leave everything default.)
1. Click Create the network

### Stack
Now you need to create a stack using a docker file. 

1. Choose Stacks from the Navigation and + Add stack.
1. Copy & pase the docker-compose.yml from below
1. Choose Deploy the stack

Once the stack says `running` you can navigate to the server's ip address making sure to include port `81`. For example: https://192.168.1.50:81

Login using these credentials and change your email and your password to something secure:

```
Email address: admin@example.com
Password: changeme
```

```
version: "3"
services:
  app:
    image: "jc21/nginx-proxy-manager:latest"
    hostname: npm
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - "80:80" # Public HTTP Port
      - "443:443" # Public HTTPS Port
      - "81:81" # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP

    # Uncomment the next line if you uncomment anything in the section
    # environment:
    # Uncomment this if you want to change the location of
    # the SQLite DB file within the container
    # DB_SQLITE_FILE: "/data/database.sqlite"

    # Uncomment this if IPv6 is not enabled on your host
    # DISABLE_IPV6: 'true'

    volumes:
      - data:/data
      - letsencrypt:/etc/letsencrypt

    healthcheck:
      test: ["CMD", "/bin/check-health"]
      interval: 10s
      timeout: 3s
    networks:
      - proxy

      
volumes:
  data:
  letsencrypt:
  
networks:
  proxy:
    external: true
```