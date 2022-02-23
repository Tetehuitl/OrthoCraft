---
title: iCloud SMTP settings
description: 
published: true
date: 2022-02-23T13:42:23.968Z
tags: 
editor: markdown
dateCreated: 2022-02-23T13:35:50.384Z
---


IMAP information for the incoming mail server

```
    Server name: imap.mail.me.com
    SSL Required: Yes
    If you see an error message when using SSL, try using TLS instead.
    Port: 993
    Username: This is usually the name part of your iCloud email address (for example, emilyparker, not emilyparker@icloud.com). If your email client can't connect to iCloud using just the name part of your iCloud email address, try using the full address.
    Password: Generate an app-specific password.
```

SMTP information for the outgoing mail server

```
    Server name: smtp.mail.me.com
    SSL Required: Yes
    If you see an error message when using SSL, try using TLS or STARTTLS instead.
    Port: 587
    SMTP Authentication Required: Yes
    Username: Your full iCloud email address (for example, emilyparker@icloud.com, not emilyparker)
    Password: Use the app-specific password that you generated when you set up the incoming mail server.
```
