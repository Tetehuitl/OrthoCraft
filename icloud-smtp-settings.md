---
title: iCloud SMTP settings
description: 
published: true
date: 2022-02-23T14:01:15.098Z
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
    Username: This is usually the name part of your iCloud email address (for example, emilyparker, not emilyparker@icloud.com).
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
