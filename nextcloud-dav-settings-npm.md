---
title: Nextcloud webdav / carddav settings for Nginx Proxy Manger
description: 
published: true
date: 2022-02-23T13:20:23.574Z
tags: 
editor: markdown
dateCreated: 2022-02-23T13:20:23.574Z
---

To get webdav and cardave to route properly change the lines in the .htaccess file.

```
RewriteRule ^\.well-known/carddav https://your_site_address/remote.php/dav/ [R=301,L]
RewriteRule ^\.well-known/caldav https://your_site_address/remote.php/dav/ [R=301,L]
```