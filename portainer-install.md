---
title: Portainer.io Setup
description: 
published: true
date: 2022-02-23T13:16:55.077Z
tags: 
editor: markdown
dateCreated: 2022-02-23T13:16:55.077Z
---

Portainer is a browser based manager for docker. 

### Setup
First create a volume to store settings.

```
docker volume create portainer_data
```

Then run this command to download and run the container.

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:2.11.1
```

Navigate here and accept the self-signed certificate.

```
https://localhost:9443
```