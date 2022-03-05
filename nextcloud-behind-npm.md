---
title: Nextcloud behind Nginx Proxy Manager
description: 
published: true
date: 2022-02-23T13:21:48.687Z
tags: 
editor: markdown
dateCreated: 2022-02-23T13:21:46.712Z
---

```
version: '3'

services:
  db:
    image: mariadb:10.6
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW --innodb-file-per-table=1 --skip-innodb-read-only-compressed
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
    networks:
      - backend

  app:
    image: nextcloud
    hostname: nextcloud
    restart: always
    volumes:
      - nextcloud:/var/www/html
    environment:
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
      - REDIS_HOST=redis
      - PHP_MEMORY_LIMIT=2G
      - PHP_UPLOAD_LIMIT=5G
#      - APACHE_DISABLE_REWRITE_IP=1
#      - TRUSTED_PROXIES=npm
      - OVERWRITEHOST=nc.orthocraft.net
      - OVERWRITEPROTOCOL=https
      - OVERWRITECLIURL=https://nc.orthocraft.net/
#      - OVERWRITEWEBROOT=/
#      - OVERWRITECONDADDR=
    depends_on:
      - db
      - redis
    networks:
      - backend
      - proxy

      
  redis:
    image: redis:alpine
#    entrypoint: redis-server --appendonly yes
    restart: always
    depends_on:
      - db
    networks:
      - backend

  cron:
    image: nextcloud:fpm-alpine
    restart: always
    volumes:
      - nextcloud:/var/www/html
    entrypoint: /cron.sh
    depends_on:
      - db
      - redis
    networks:
      - backend
     


volumes:
  db:
  nextcloud:

networks:
  backend:
  proxy:
    external: true
```